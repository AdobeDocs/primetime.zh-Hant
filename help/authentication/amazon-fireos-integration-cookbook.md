---
title: Amazon FireOS整合逐步指南
description: Amazon FireOS整合逐步指南
exl-id: 1982c485-f0ed-4df3-9a20-9c6a928500c2
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Amazon FireOS整合逐步指南 {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>


## 簡介 {#intro}

本檔案說明程式設計師的上層應用程式可透過Amazon FireOS AccessEnabler程式庫公開的API實施的權益工作流程。

Amazon FireOS的Adobe Primetime驗證許可權解決方案最終分為兩個網域：

- UI網域 — 這是實作UI並使用AccessEnabler資料庫所提供之服務來提供對受限制內容的存取的上層應用程式層。
- AccessEnabler網域 — 這是軟體權利檔案工作流程的實作方式，其形式為：
   - 對Adobe後端伺服器發出的網路呼叫
   - 與驗證和授權工作流程相關的商業邏輯規則
   - 管理各種資源及處理工作流程狀態（例如權杖快取）

AccessEnabler網域的目標是隱藏軟體權利檔案工作流程的所有複雜性，並（透過AccessEnabler資料庫）提供一組簡單軟體權利檔案原件，供您實作軟體權利檔案工作流程：

1. 設定要求者身分
1. 檢查並取得特定身分提供者的驗證
1. 檢查並取得特定資源的授權
1. 登出

AccessEnabler的網路活動發生在不同的執行緒中，因此不會封鎖UI執行緒。 因此，兩個應用程式網域之間的雙向通訊通道必須遵循完全非同步模式：

- UI應用程式層透過AccessEnabler程式庫公開的API呼叫，將訊息傳送至AccessEnabler網域。
- AccessEnabler會透過AccessEnabler通訊協定（UI層向AccessEnabler程式庫註冊）中包含的回呼方法回應UI層。

## 權益流程 {#entitlement}

1. [必要條件](#prereqs)
1. [啟動流程](#startup_flow)
1. [驗證流程](#authn_flow)
1. [授權流程](#authz_flow)
1. [檢視媒體流程](#media_flow)
1. [登出流程](#logout_flow)

 

### A.必要條件 {#prereqs}

1. 建立回呼函式：
   - [&#39;setRequestorComplete()&#39;](#$setRequestorComplete)

      - 觸發者 `setRequestor()`，會傳回成功或失敗。     「成功」表示您可以繼續權益呼叫。
   - [displayProviderDialog(mvpd)](#$displayProviderDialog)

      - 觸發者 `getAuthentication()` 只有當使用者尚未選取提供者(MVPD)且尚未驗證時。 此 `mvpds` parameter是使用者可用的提供者陣列。
   - [&#39;setAuthenticationStatus(status， reason)&#39;](#$setAuthNStatus)

      - 觸發者 `checkAuthentication()` 每次。 觸發者 `getAuthentication()` 僅當使用者已經驗證並已選取提供者時。

      - 傳回的狀態已驗證或未驗證，原因說明驗證失敗或登出動作。
   - [navigateToUrl(url)](#$navigateToUrl)

      - 在AmazonFireOS SDK中忽略，方法用於Android平台，觸發者為 `getAuthentication()` 在使用者選取MVPD之後。  此 `url` 引數會提供MVPD登入頁面的位置。
   - [&#39;sendTrackingData(event， data)&#39;](#$sendTrackingData)

      - 觸發者 `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
此 `event` 引數指出已發生的權益事件； `data` parameter是與事件相關的值清單。 
   - [&#39;setToken(token， resource)&#39;](#$setToken)

      - 觸發者 `checkAuthorization()` 和 `getAuthorization()` 成功授權後檢視資源。
      - 此 `token` 引數是短期媒體代號；而 `resource` 引數是使用者有權檢視的內容。
   - [&#39;tokenRequestFailed(resource， code， description)&#39;](#$tokenRequestFailed)

      - 觸發者 `checkAuthorization()` 和 `getAuthorization()` 授權失敗後。
      - 此 `resource` 引數是使用者嘗試檢視的內容； `code` parameter是錯誤碼，指出發生的失敗型別； `description` 引數說明與錯誤碼相關的錯誤。
   - [&#39;selectedProvider(mvpd)&#39;](#$selectedProvider)

      - 觸發者 `getSelectedProvider()`.
      - 此 `mvpd` parameter提供使用者選取之提供者的相關資訊。
   - [&#39;setMetadataStatus(metadata， key， arguments)&#39;](#$setMetadataStatus)

      - 觸發者 `getMetadata().`
      - 此 `metadata` 引數會提供您要求的特定資料； `key` parameter是中使用的金鑰 `getMetadata()` 要求；以及 `arguments` parameter是傳遞至的相同字典 `getMetadata()`.
   - [&#39;preauthorizedResources(resources)&#39;](#$preauthResources)

      - 觸發者 `checkPreauthorizedResources()`.
      - 此 `authorizedResources` 引數會顯示使用者有權檢視的資源。\
          










![](assets/android-entitlement-flows.png)\
 

### B.啟動流程 {#startup_flow}

1. 啟動上層應用程式。
1. 啟動Adobe Primetime驗證
   1. 呼叫 [`getInstance`](#$getInstance) 建立Adobe Primetime驗證AccessEnabler的單一執行個體。

      - **相依性：** Adobe Primetime驗證原生Amazon FireOS程式庫(AccessEnabler)
   2. 呼叫` setRequestor()` 建立程式設計師的身分識別；傳入程式設計師的 `requestorID` 和（可選）Adobe Primetime驗證端點的陣列。

      - **相依性：** 有效的Adobe Primetime驗證請求者ID (請洽詢Adobe Primetime驗證帳戶管理員以安排此作業。)

      - **觸發器：** setRequestorComplete()回呼

   在完全建立請求者身分之前，無法完成任何權益請求。 這實際上意味著setRequestor()仍在執行時，所有後續的權益請求(例如`checkAuthentication()`)已封鎖。

   您有兩個實作選項：請求者識別資訊傳送至後端伺服器後，UI應用程式層可以選擇下列兩種方法之一：</p>

   1. 等待觸發 `setRequestorComplete()` 回呼（AccessEnabler委派的一部分）。  此選項最能確定 `setRequestor()` 已完成，因此建議用於大部分實作。

   1. 繼續而不等待觸發 `setRequestorComplete()` 回撥，並開始發出軟體權利檔案請求。 這些呼叫(checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、logout)會由AccessEnabler程式庫排入佇列，這會在以下動作之後進行實際的網路呼叫： `setRequestor()`. 例如，如果網路連線不穩定，此選項偶爾會中斷。




1. 呼叫 [checkAuthentication()](#$checkAuthN) 檢查現有的驗證，而不啟動完整的驗證流程。  如果此呼叫成功，您可以直接繼續進行授權流程。  如果沒有，請繼續進行驗證流程。

- **相依性：** 成功呼叫 `setRequestor()` （此相依性也適用於所有後續呼叫）。

- **觸發器：** setAuthenticationStatus()回呼

### C.驗證流程 {#authn_flow}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 以啟動驗證流程，或取得使用者已驗證的確認。 

   **觸發器：**  

   - setAuthenticationStatus()回呼（如果使用者已經驗證）。  在此情況下，請直接前往 [授權流程](#authz_flow).
   - displayProviderDialog()回呼（如果使用者尚未驗證）。  

1. 向使用者呈現傳送至的提供者清單 `displayProviderDialog()`.

1. 使用者選取提供者後，WebView會開啟提供者頁面，供使用者登入

   **注意：** 此時，使用者有機會取消驗證流程。 如果發生這種狀況，AccessEnabler會清理其內部狀態，並重設驗證流程。

1. 使用者成功登入後，WebView將會關閉。

1. 呼叫 `getAuthenticationToken(),` 會指示AccessEnabler從後端伺服器擷取驗證Token。 

1. [可選] 呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 以檢查使用者有權檢視哪些資源。 此 `resources` parameter是與使用者的驗證Token相關聯的受保護資源陣列。\
   **觸發器：** `preAuthorizedResources()` callback\
   **執行點：** 完成驗證流程後

1. 如果驗證成功，請繼續進行授權流程。

 

### D.授權流程 {#authz_flow}

1. 呼叫 [`getAuthorization()`](#$getAuthZ) 以啟動授權流程。

   相依性：與MVPD議定的有效ResourceID。

   **注意：** ResourceIDs應與任何其他裝置或平台上使用的相同，且在MVPD間將相同。

1. 驗證驗證和授權。

   - 如果 `getAuthorization()` 呼叫成功：使用者擁有有效的AuthN和AuthZ權杖（使用者已驗證並獲授權觀看要求的媒體）。
   - 若 `getAuthorization()` 失敗：檢查擲回的例外狀況，以判斷其型別（AuthN、AuthZ或其他專案）：
      - 如果是驗證(AuthN)錯誤，則重新啟動驗證流程。
      - 如果是授權(AuthZ)錯誤，則使用者無權觀看請求的媒體，並且應向使用者顯示某種錯誤訊息。
      - 如果有其他型別的錯誤（連線錯誤、網路錯誤等） 然後向使用者顯示適當的錯誤訊息。

1. 驗證短媒體權杖。

   使用Adobe Primetime驗證媒體權杖驗證器程式庫，驗證從傳回的短期媒體權杖 `getAuthorization()` 以上呼叫：

   - 如果驗證成功：為使用者播放要求的媒體。
   - 如果驗證失敗： AuthZ權杖無效，應拒絕媒體請求，並向使用者顯示錯誤訊息。

1. 返回正常的應用程式流程。

### E.檢視Media流程 {#media_flow}

1. 使用者選取要檢視的媒體。
1.  媒體是否受到保護？  您的應用程式會檢查選取的媒體是否受到保護：
   - 如果選取的媒體受到保護，您的應用程式會啟動 [授權流程](#authz_flow) 以上。
   - 如果選取的媒體未受到保護，則播放該使用者的媒體。

### F.登出流程 {#logout_flow}

1. 呼叫 [`logout()`](#$logout) 將使用者登出。 \
   AccessEnabler會清除使用者在共用單一登入之所有要求者上，為目前的MVPD取得的所有快取值和權杖。 清除快取之後，AccessEnabler會進行伺服器呼叫以清除伺服器端工作階段。  請注意，由於伺服器呼叫可能會導致SAML重新導向至IdP （這允許IdP端的工作階段清理），此呼叫必須在所有重新導向之後。 因此，此呼叫將在WebView控制項中處理，使用者看不到該控制項。

   **注意：** 登出流程與驗證流程的不同之處在於，使用者不需要以任何方式與WebView互動。 因此，在登出過程中，可以（而且建議）隱藏WebView控制項（亦即：隱藏）。
