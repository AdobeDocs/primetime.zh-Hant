---
title: Android SDK指南
description: Android SDK指南
exl-id: 7f66ab92-f52c-4dae-8016-c93464dd5254
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# Android SDK指南 {#android-sdk-cookbook}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 導言 {#intro}

本文檔介紹程式設計師的高級應用程式可以通過Android AccessEnabler庫公開的API實現的權利工作流。


針對Android的Adobe Primetime認證授權解決方案最終分為兩個域：

- UI域 — 這是實現UI並使用AccessEnabler庫提供的服務提供對受限內容的訪問的上層應用層。
- AccessEnabler域 — 在此處，權利工作流以以下形式實現：
   - 對Adobe後端伺服器進行的網路呼叫
   - 與身份驗證和授權工作流相關的業務邏輯規則
   - 管理各種資源和處理工作流狀態（例如令牌快取）

AccessEnabler域的目標是隱藏權利工作流的所有複雜性，並向上層應用程式（通過AccessEnabler庫）提供一組簡單的權利原語，您可以使用這些原語來實施權利工作流：

1. 設定請求者標識
1. 檢查並獲取針對特定身份提供程式的身份驗證
1. 檢查並獲取特定資源的授權
1. 註銷

AccessEnabler的網路活動發生在不同的線程中，因此UI線程從不被阻止。 因此，兩個應用域之間的雙向通信通道必須遵循完全非同步模式：

- UI應用層通過AccessEnabler庫公開的API調用向AccessEnabler域發送消息。
- AccessEnabler通過AccessEnabler協定中包含的回調方法對UI層作出響應，UI層在AccessEnabler庫中註冊了該回調方法。

## 權利流 {#entitlement}

1. [先決條件](#prereqs)
1. [啟動流](#startup_flow)
1. [驗證流](#authn_flow)
1. [授權流](#authz_flow)
1. [查看媒體流](#media_flow)
1. [註銷流](#logout_flow)

 

### 答：先決條件 {#prereqs}

1. 建立回調函式：
   - [&#39;setRequestorComplete()&#39;](#$setRequestorComplete)

      觸發者 `setRequestor()`，返回成功或失敗。  \
      成功表示您可以繼續權利調用。

   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      觸發者 `getAuthentication()` 僅當用戶尚未選擇提供程式(MVPD)且尚未驗證時，才可使用。  \
      的 `mvpds` 參數是用戶可用的提供程式陣列。

   - [&#39;setAuthenticationStatus(status, errorcode)&#39;](#$setAuthNStatus)

      觸發者 `checkAuthentication()` 每次。\
      觸發者 `getAuthentication()` 僅當用戶已經過身份驗證並已選擇提供程式時。

      返回的狀態是成功或失敗，錯誤代碼描述失敗的類型。

   - [導航至URL(url)](#$navigateToUrl)

      觸發者 `getAuthentication()` 在用戶選擇MVPD後。 的 `url` 參數提供MVPD登錄頁的位置。

   - [&#39;sendTrackingData（事件，資料）&#39;](#$sendTrackingData)

      觸發者 `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`。\
      的 `event` 參數指示發生了哪些權利事件；這樣 `data` 參數是與事件相關的值清單。 

   - [&#39;setToken(token, resource)&#39;](#$setToken)

      觸發者 `checkAuthorization()` 和 `getAuthorization()` 在成功授權查看資源後。\
      的 `token` 參數是短壽命的媒體令牌；這樣 `resource` 參數是用戶有權查看的內容。

   - [&#39;tokenRequestFailed（資源，代碼，說明）&#39;](#$tokenRequestFailed)

      觸發者 `checkAuthorization()` 和 `getAuthorization()` 授權失敗。\
      的 `resource` 參數是用戶嘗試查看的內容；這樣 `code` 參數是錯誤代碼，指示出現了哪種類型的故障；這樣 `description` 參數描述與錯誤代碼相關的錯誤。

   - [&#39;selectedProvider(mvpd)&#39;](#$selectedProvider)

      觸發者 `getSelectedProvider()`。\
      的 `mvpd` 參數提供有關用戶選擇的提供程式的資訊。

   - [&#39;setMetadataStatus（元資料、鍵、參數）&#39;](#$setMetadataStatus)

      觸發者 `getMetadata().`\
      的 `metadata` 參數提供您請求的特定資料；這樣 `key` 參數是 `getMetadata()` 請求；和 `arguments` 參數是傳遞給的同一字典 `getMetadata()`。

   - [&#39;preauthorizedResources(resources)&#39;](#$preauthResources)

      觸發者 `checkPreauthorizedResources()`。\
      的 `authorizedResources` 參數顯示用戶有權查看的資源。\
       

![](assets/android-entitlement-flows.png)\
 

### B啟動流 {#startup_flow}

1. 啟動高級應用程式。
1. 啟動Adobe Primetime身份驗證

   a.呼叫 [`getInstance`](#$getInstance) 建立Adobe Primetime身份驗證AccessEnabler的單個實例。

   - **依賴關係：** Adobe Primetime驗證本機Android庫(AccessEnabler)

   b.呼叫` setRequestor()` 確定程式設計師的身份；程式設計師 `requestorID` 和（可選）一組Adobe Primetime驗證端點。

   - **依賴關係：** 有效的Adobe Primetime驗證請求者ID\
      (與您的Adobe Primetime身份驗證客戶經理合作安排。)

   - **觸發器：** setRequestorComplete()回調

   | 注釋 |  |
   | --- | --- |  
   | ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/icons/1313859077_lightbulb.png) | 在完全建立請求者身份之前，無法完成任何權利請求。 這實際上意味著，儘管setRequestor()仍在運行，但所有後續權利請求(例如， `checkAuthentication()`)。<br><br>您有兩個實施選項：一旦請求者標識資訊被發送到後端伺服器，UI應用層可以選擇以下兩種方法之一：<br><br>1。  等待觸發 `setRequestorComplete()` 回調（AccessEnabler委託的一部分）。  此選項最確定地 `setRequestor()` 已完成，因此建議用於大多數實施。<br>2.  繼續，而不等待觸發 `setRequestorComplete()` 回調，並開始發出權利請求。 這些調用(checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、logout)由AccessEnabler庫排隊，該庫將在AccessEnabler之後進行實際的網路調用 `setRequestor(). `例如，如果網路連接不穩定，則有時可能會中斷此選項。 |

1. 呼叫 [checkAuthentication()](#$checkAuthN) 檢查現有驗證而不啟動完整驗證流。   如果此調用成功，則可以直接進入授權流。  否則，繼續驗證流。

   - **依賴關係：** 成功調用 `setRequestor()` （此依賴關係也適用於所有後續調用）。

   - **觸發器：** setAuthenticationStatus()回調

 

### C.認證流 {#authn_flow}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流，或獲得用戶已經驗證的確認。 \
   **觸發器：**  
   - 如果用戶已經經過身份驗證，則返回setAuthenticationStatus()回調。  在這種情況下，請直接轉到 [授權流](#authz_flow)。
   - 如果用戶尚未通過身份驗證，則使用displayProviderDialog()回調。  

1. 向用戶顯示發送到的提供程式清單 `displayProviderDialog()`。

1. 用戶選擇提供程式後，從 `navigateToUrl()` 回叫。  開啟WebView並將該WebView控制項定向到URL。   

1. 通過在上一步中實例化的WebView，用戶將登陸到MVPD的登錄頁並輸入登錄憑據。 在WebView中執行了多個重定向操作。\
    

   **注：** 此時，用戶有機會取消驗證流。 如果發生這種情況，則您的UI層負責通過調用將此事件通知AccessEnabler `setSelectedProvider()` 與 `null` 的雙曲餘切值。 這允許AccessEnabler清除其內部狀態並重置身份驗證流。

1. 用戶成功登錄後，您的應用層將檢測到「自定義重定向URL」的載入(即： [http://adobepass.android.app](http://adobepass.android.app/))。 此自定義URL實際上是無效的URL，它不用於WebView載入。 這是驗證流已完成且需要關閉WebView的信號。

1. 關閉WebView控制項並調用 `getAuthenticationToken()`，指示AccessEnabler從後端伺服器檢索身份驗證令牌。 

1. [可選] 呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。 的 `resources` 參數是與用戶的驗證令牌關聯的受保護資源的陣列。\
   **觸發器：** `preAuthorizedResources()` 回調\
   **執行點：** 完成身份驗證流程後

1. 如果驗證成功，請繼續到授權流。

 

### D授權流 {#authz_flow}

1. 呼叫 [getAuthorization()](#$getAuthZ) 啟動授權流。

   依賴關係：與MVPD一致的有效資源ID。

   **注：** 資源ID應與任何其他設備或平台上使用的ID相同，並且在MVPD上也相同。

1. 驗證身份驗證和授權。

   - 如果 `getAuthorization()` 呼叫成功：用戶具有有效的AuthN和AuthZ令牌（用戶已通過身份驗證並被授權監視請求的媒體）。
   - 如果 `getAuthorization()` 失敗：檢查拋出的異常以確定其類型（AuthN、AuthZ或其他）:
      - 如果是驗證(AuthN)錯誤，則重新啟動驗證流。
      - 如果是授權(AuthZ)錯誤，則用戶無權監視請求的媒體，應向用戶顯示某種錯誤消息。
      - 如果存在其他類型的錯誤（連接錯誤、網路錯誤等） 然後向用戶顯示相應的錯誤消息。

1. 驗證短媒體令牌。\
   使用Adobe Primetime驗證媒體令牌驗證器庫驗證從 `getAuthorization()` 以上呼叫：

   - 如果驗證成功：為用戶播放請求的媒體。
   - 如果驗證失敗：AuthZ令牌無效，應拒絕媒體請求，並應向用戶顯示錯誤消息。

1. 返回到正常應用程式流。

### E.查看媒體流 {#media_flow}

1. 用戶選擇要查看的媒體。
2.  介質是否受到保護？  您的應用程式將檢查所選介質是否受保護：
   - 如果選定的介質受保護，應用程式將啟動 [授權流](#authz_flow) 上。
   - 如果選定的介質未受保護，則播放用戶的介質。

 

### F.註銷流 {#logout_flow}

1. 呼叫 [`logout()`](#$logout) 將用戶註銷。 \
   AccessEnabler將清除當前請求者以及具有單一登錄的請求者的當前MVPD的所有快取值和令牌。 清除快取後，AccessEnabler會調用伺服器來清除伺服器端會話。  請注意，由於伺服器調用可能導致SAML重定向到IdP（這允許在IdP端進行會話清理），因此此調用必須遵循所有重定向。 因此，必須在WebView控制項內處理此調用。

   a.遵循與身份驗證工作流相同的模式，AccessEnabler域向UI應用層發出請求(通過`navigateToUrl()` 回調)建立WebView控制項，並指示該控制項在後端伺服器上載入註銷終結點的URL。

   b.同樣，UI必須監視WebView控制項的活動，並檢測當控制項在多次重定向過程中載入應用程式的自定義URL(即： [http://adobepass.android.app/](http://adobepass.android.app/))。 一旦發生此事件，UI應用層將關閉WebView並完成註銷過程。

   **注：** 註銷流與驗證流不同，因為用戶不需要以任何方式與WebView交互。 UI應用層使用WebView來確保所有重定向都得到遵守。 因此，在註銷過程中可能（並建議）使WebView控制項不可見（即隱藏）。

 

### 使用多個MVPD和註銷登錄的用戶流 {#user_flows}

[這裡](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AndroidSSOUserFlows.pdf) 您有一個文檔，描述使用多個MVPD時的行為以及用戶從應用程式註銷時發生的情況。

使用Android SDK版本>= 2.0.0時，可使用上述行為。
