---
title: iOS/tvOS逐步指南
description: iOS/tvOS逐步指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# iOS/tvOS SDK逐步指南 {#iostvos-sdk-cookbook}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro}

本文檔描述了程式設計師的高級應用程式可以通過iOS/tvOS AccessEnabler庫公開的API實施的權限工作流。

iOS/tvOS的Adobe Primetime驗證權限解決方案最終分為兩個網域：

* UI域 — 這是實現UI的高級應用層，使用AccessEnabler庫提供的服務來提供對受限內容的訪問。

* AccessEnabler域 — 在此處，權限工作流以以下形式實施：

   * 對Adobe後端伺服器進行的網路呼叫
   * 與驗證和授權工作流程相關的業務邏輯規則
   * 管理各種資源並處理工作流程狀態（例如權杖快取）

AccessEnabler域的目標是隱藏權限工作流的所有複雜內容，並（通過AccessEnabler庫）向上層應用程式提供一組簡單權限原語，您可以用這些原語來實施權限工作流：

1. 設定請求者身分
1. 檢查並獲取對特定身份提供程式的身份驗證
1. 檢查並獲取特定資源的授權
1. 登出
1. Apple SSO通過批准Apple VSA框架流動

AccessEnabler的網路活動發生在其自身線程中，因此UI線程不會被阻止。 因此，兩個應用程式網域之間的雙向通訊通道必須遵循完全非同步的模式：

* UI應用層通過AccessEnabler庫公開的API調用將消息發送到AccessEnabler域。
* AccessEnabler通過AccessEnabler協定中包含的回調方法響應UI層，UI層向AccessEnabler庫註冊該回調方法。

## 設定訪客ID {#visitorIDSetup}

設定 [Marketing CloudvisitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) 從分析的角度來看，值非常重要。 設定visitorID值後，SDK會傳送此資訊以及每個網路呼叫，而Adobe Primetime驗證伺服器會收集此資訊。 日後，您將能將來自Adobe Primetime驗證服務的分析與其他應用程式或網站的分析報表建立關聯。 如需如何設定visitorID的資訊，請參閱 [此處](#setOptions).

## 權利流 {#entitlement}

答：  [必要條件](#prereqs) </br>
B.  [啟動流程](#startup_flow) </br>
C.  [使用Apple SSO的驗證流程](#authn_flow_wo_applesso)  </br>
D.  [iOS上使用Apple SSO的驗證流程](#authn_flow_with_applesso) </br>
E.  [tvOS上使用Apple SSO的驗證流程](#authn_flow_with_applesso_tvOS) </br>
F.  [授權流程](#authz_flow) </br>
G.  [檢視媒體流量](#media_flow) </br>
H.  [沒有Apple SSO的登出流程](#logout_flow_wo_AppleSSO) </br>
我。  [使用Apple SSO登出流程](#logout_flow_with_AppleSSO) </br>


### A.先決條件 {#prereqs}

1. 建立回呼函式：
   * `setRequestorComplete()` </br>
   * 觸發者 [setRequestor()](#$setReq)，則傳回成功或失敗。 </br>
   * 成功表示您可以繼續進行權限呼叫。

   * [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      * 觸發者 [`getAuthentication()`](#$getAuthN) 僅當使用者尚未選取提供者(MVPD)且尚未驗證時。 </br>
      * 此 `mvpds` 參數是使用者可用的提供者陣列。
   * `setAuthenticationStatus(status, errorcode)` </br>
      * 觸發者 `checkAuthentication()` 每次。 </br>
      * 觸發者 [`getAuthentication()`](#$getAuthN) 只有在使用者已驗證且已選取提供者時。 </br>
      * 傳回的狀態為成功或失敗，errorcode描述失敗的類型。
   * [`navigateToUrl(url)`](#$nav2url) </br>
      * 觸發者 [`getAuthentication()`](#$getAuthN) 使用者選取MVPD後。 此 `url` 參數提供MVPD登入頁面的位置。
   * `sendTrackingData(event, data)` </br>
      * 觸發者 `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.
      * 此 `event` 參數指示發生了哪些權利事件；the `data` 參數是與事件相關的值清單。 
   * `setToken(token, resource)`

      * 觸發者 [checkAuthorization()](#checkAuthZ) 和 [getAuthorization()](#$getAuthZ) 在成功授權以檢視資源後。
      * 此 `token` 參數是短期媒體代號；the `resource` 參數是使用者有權檢視的內容。
   * `tokenRequestFailed(resource, code, description)` </br>
      * 觸發者 [checkAuthorization()](#checkAuthZ) 和 [getAuthorization()](#$getAuthZ) 授權失敗後。
      * 此 `resource` 參數是使用者嘗試檢視的內容；the `code` 參數是錯誤碼，指出發生的故障類型；the `description` 參數描述了與錯誤代碼相關的錯誤。
   * `selectedProvider(mvpd)` </br>
      * 觸發者 [`getSelectedProvider()`](#getSelProv).
      * 此 `mvpd` 參數提供有關用戶選擇的提供程式的資訊。
   * `setMetadataStatus(metadata, key, arguments)`
      * 觸發者 `getMetadata().`
      * 此 `metadata` 參數提供您請求的特定資料；the `key` 參數是 [getMetadata()](#getMeta) 要求；和 `arguments` 參數是傳遞至的相同字典 [getMetadata()](#getMeta).
   * [&#39;preauthorizedResources(authorizedResources)&#39;](#preauthResources)

      * 觸發者 [`checkPreauthorizedResources()`](#checkPreauth).

      * 此 `authorizedResources` 參數會提供使用者有權檢視的資源。
   * [&#39;presentTvProviderDialog(viewController)&#39;](#presentTvDialog)

      * 觸發者 [getAuthentication()](#getAuthN) 當目前要求者至少支援具有SSO支援的MVPD時。
      * viewController參數是Apple SSO對話框，需要在主視圖控制器上顯示。
   * [&#39;disclessTvProviderDialog(viewController)&#39;](#dismissTvDialog)

      * 由使用者動作觸發(從Apple SSO對話方塊中選取「取消」或「其他電視提供者」)。
      * viewController參數是Apple SSO對話框，需要從主視圖控制器中關閉。











![](assets/iOS-flows.png)

### B.啟動流程 {#startup_flow}

1. 啟動高級應用程式。</br>
1. 啟動Adobe Primetime驗證 </br>

   a.呼叫 [`init`](#$init) 建立Adobe Primetime身份驗證AccessEnabler的單個實例。
   * **相依性：** Adobe Primetime驗證原生iOS/tvOS Library(AccessEnabler)
   b.呼叫 `setRequestor()` 建立程式設計師的身份；在程式設計師的 `requestorID` 和（可選）Adobe Primetime驗證端點的陣列。 對於tvOS，您也需要提供公開金鑰和機密。 請參閱 [無客戶端文檔](#create_dev) 以取得詳細資訊。

   * **相依性：** 有效的Adobe Primetime驗證RequestorID(請與您的Adobe Primetime驗證帳戶管理員合作安排)。

   * **觸發器：**
      [setRequestorComplete()](#$setReqComplete) 回呼。
   >[!NOTE]
   >
   >在完全建立請求者身分之前，無法完成任何權限請求。 這實際上意味著， [`setRequestor()`](#$setReq)  仍在執行中，所有後續的權限要求。 例如， [`checkAuthentication()`](#checkAuthN) 被阻止。

   您有兩個實作選項：一旦請求者識別資訊傳送至後端伺服器，UI應用層可選擇下列兩種方法之一： </br>

   1. 等待觸發 [`setRequestorComplete()`](#setReqComplete) callback（AccessEnabler委派的一部分）。 這個選項最能確定 [`setRequestor()`](#$setReq) 已完成，因此建議用於大部分實作。

   1. 繼續，而不等待 [`setRequestorComplete()`](#setReqComplete) 回呼，然後開始發出權限要求。 這些調用(checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、logout)由AccessEnabler庫排入隊列，這些調用將在 [`setRequestor()`](#$setReq). 例如，如果網路連接不穩定，此選項偶爾會中斷。



1. 呼叫 `checkAuthentication()` 來檢查現有驗證，而不啟動完整的驗證流程。  如果此呼叫成功，您可以直接前往授權流程。 如果沒有，請繼續進行驗證流程。

   * **相依性：** 成功呼叫 [setRequestor()](#$setReq) （此相依性也會套用至所有後續呼叫）。

   * **觸發器：** [setAuthenticationStatus()](#$setAuthNStatus) 回呼。


### C.無Apple SSO的驗證流 {#authn_flow_wo_applesso}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流程，或取得使用者已通過驗證的確認。

   **觸發器：**

   * 此 [setAuthenticationStatus()](#$setAuthNStatus) 回呼，如果使用者已通過驗證。 在此情況下，請直接前往 [授權流程](#authz_flow).

   * 此 [displayProviderDialog()](#$dispProvDialog) 回呼，若使用者尚未驗證。

1. 向用戶顯示發送到的提供程式清單
   [`displayProviderDialog()`](#dispProvDialog).

1. 使用者選取提供者後，從 `navigateToUrl:` 或 `navigateToUrl:useSVC:` 回呼並開啟 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器，並將該控制器導向至URL。

1. 透過 `UIWebView/WKWebView` 或 `SFSafariViewController` 在上一步驟中具現化後，使用者會登陸MVPD的登入頁面並輸入登入憑證。 控制器內發生了多個重定向操作。</br>

>[!NOTE]
>
>此時，用戶有機會取消身份驗證流。 如果發生此情況，您的UI層將負責通過呼叫將此事件通知AccessEnabler [setSelectedProvider()](#setSelProv) with `null` 作為參數。 這允許AccessEnabler清除其內部狀態並重置身份驗證流。

1. 使用者成功登入時，您的應用程式層會偵測特定自訂URL的載入。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只能將其解讀為驗證流程已完成且關閉安全的信號 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器。 若 `SFSafariViewController`控制器，才能使用由 **`application's custom scheme`** (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 **`ADOBEPASS_REDIRECT_URL`** 常數，即 `adobepass://ios.app`)。

1. 關閉UIWebView/WKWebView或SFSafariViewController控制器，並調用AccessEnabler的 `handleExternalURL:url` API方法，指示AccessEnabler從後端伺服器擷取驗證Token。

1. （可選）呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。 此 `resources` 參數是與使用者的驗證權杖相關聯的受保護資源陣列。 從用戶的MVPD獲取的授權資訊的一個用途是裝飾您的UI（例如，受保護內容旁的鎖定/解鎖符號）。

   * **觸發器：** [`preauthorizedResources()`](#preauthResources) 回撥
   * **執行點：** 完成驗證流程後

1. 如果驗證成功，請繼續執行授權流程。

### D.iOS上使用Apple SSO的驗證流程 {#authn_flow_with_applesso}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流程，或取得使用者已通過驗證的確認。
   **觸發器：**

   * 此 [presentTvProviderDialog()](#presentTvDialog) 回呼，如果使用者未驗證，且目前要求者至少在支援SSO的MVPD上具有。 如果沒有MVPD支援SSO，則會使用傳統驗證流程。

1. 在用戶選擇提供程式後，AccessEnabler庫將獲取驗證令牌，該令牌包含Apple的VSA框架提供的資訊。

1. 此 [setAuthenticationsStatus()](#setAuthNStatus) 將觸發回呼。 此時，應使用Apple SSO驗證使用者。

1. [可選] 呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。 此 `resources` 參數是與使用者的驗證權杖相關聯的受保護資源陣列。 從使用者的MVPD取得的授權資訊之一，是用來裝飾您的UI（例如，受保護內容旁的鎖定/解鎖符號）。

   * **觸發器：** [`preauthorizedResources()`](#preauthResources) 回撥
   * **執行點：** 完成驗證流程後

1. 如果驗證成功，請繼續執行授權流程。

### E.tvOS上使用Apple SSO的驗證流程 {#authn_flow_with_applesso_tvOS}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流程，或取得使用者已通過驗證的確認。
   **觸發器：**
   * 此 [`presentTvProviderDialog()`](#presentTvDialog) 回呼，如果使用者未驗證，且目前要求者至少在支援SSO的MVPD上具有。 如果沒有MVPD支援SSO，則會使用傳統驗證流程。

1. 使用者選取提供者後， [`status()`](#status_callback_implementation) 將呼叫callback。 將提供註冊代碼，AccessEnabler庫將開始輪詢伺服器以進行成功的第二螢幕驗證。

1. 如果提供的註冊代碼用於在第二個螢幕上成功驗證，則 [`setAuthenticatiosStatus()`](#setAuthNStatus) 將觸發回呼。 此時，應使用Apple SSO驗證使用者。
1. [可選] 呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。 此 `resources` 參數是與使用者的驗證權杖相關聯的受保護資源陣列。 從使用者的MVPD取得的授權資訊之一，是用來裝飾您的UI（例如，受保護內容旁的鎖定/解鎖符號）。

   * **觸發器：** [`preauthorizedResources()`](#preauthResources) 回撥

   * **執行點：** 完成驗證流程後
1. 如果驗證成功，請繼續執行授權流程。

### F.授權流程 {#authz_flow}

1. 呼叫 [getAuthorization()](#$getAuthZ) 啟動授權流程。

   * **相依性：** 與MVPD同意的有效資源ID。
   * 資源ID應與任何其他裝置或平台上使用的ID相同，且在MVPD上會相同。 如需資源ID的相關資訊，請參閱 [標識受保護的資源](/help/authentication/identify-protected-resources.md)

1. 驗證驗證和授權。

   * 若 [getAuthorization()](#$getAuthZ) 呼叫成功：使用者具有有效的AuthN和AuthZ權杖（使用者已通過驗證，且已獲授權可觀看請求的媒體）。

   * 若 [getAuthorization()](#$getAuthZ) 失敗：檢查擲回的例外狀況，以判斷其類型（AuthN、AuthZ或其他類型）:
      * 如果是驗證(AuthN)錯誤，則重新啟動驗證流程。
      * 如果是授權(AuthZ)錯誤，則用戶無權觀看請求的媒體，應向用戶顯示某種錯誤消息。
      * 如果有其他類型的錯誤（連線錯誤、網路錯誤等）, 然後向用戶顯示相應的錯誤消息。

1. 驗證短媒體代號。\
   使用Adobe Primetime驗證媒體代號驗證程式程式庫，驗證從 [getAuthorization()](#$getAuthZ) 呼叫上述：

   * 如果驗證成功：為用戶播放請求的媒體。
   * 如果驗證失敗：AuthZ代號無效，應拒絕媒體要求，且應向使用者顯示錯誤訊息。


1. 返回正常應用程式流。

### G.檢視媒體流量 {#media_flow}

1. 使用者選取要檢視的媒體。
1. 介質是否受到保護？ 您的應用程式檢查所選介質是否受到保護：

   * 如果所選介質受保護，則應用程式將啟動 [授權流程](#authz_flow) 上。

   * 如果所選介質未受保護，則為用戶播放該介質。

### H.沒有Apple SSO的登出流程 {#logout_flow_wo_AppleSSO}

1. 呼叫 [`logout()`](#$logout) 將用戶註銷。 AccessEnabler會清除所有快取值和令牌。 清除快取後，AccessEnabler會發出伺服器呼叫以清除伺服器端會話。 請注意，由於伺服器呼叫可能導致SAML重新導向至IdP（這允許在IdP端清除工作階段），因此此呼叫必須遵循所有重新導向。 因此，必須在UIWebView/WKWebView或SFSafariViewController控制器內處理此呼叫。

   a.按照與身份驗證工作流相同的模式，AccessEnabler域通過 `navigateToUrl:` 或 `navigateToUrl:useSVC:` 回呼，建立UIWebView/WKWebView或SFSafariViewController控制器，並指示載入回呼中提供的URL `url` 參數。 這是後端伺服器上登出端點的URL。

   b.您的應用程式必須監控 `UIWebView/WKWebView or SFSafariViewController` controller並偵測載入特定自訂URL的時機，因為它經過數個重新導向。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只必須將其解讀為已完成登出流程且關閉 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器。 當控制器載入此特定自訂URL時，您的應用程式必須關閉 `UIWebView/WKWebView or SFSafariViewController` 控制器並調用AccessEnabler的 `handleExternalURL:url`API方法。 若 `SFSafariViewController`控制器，才能使用由 **`application's custom scheme`** (例如， `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 **`ADOBEPASS_REDIRECT_URL`**  常數，即 `adobepass://ios.app`)。

   >[!NOTE]
   >
   >註銷流與驗證流不同，因為用戶不需要以任何方式與UIWebView/WKWebView或SFSafariViewController交互。 UI應用層使用UIWebView/WKWebView或SFSafariViewController來確保遵循所有重定向。 因此，在註銷過程中，可以（並建議）使控制器不可見（即隱藏）。


### I.使用Apple SSO登出流程 {#logout_flow_with_AppleSSO}

1. 呼叫 [`logout()`](#$logout) 將用戶註銷。
1. 此 [status()](#status_callback_implementation) 將使用id VSA203呼叫callback。
1. 還應指示用戶從系統設定中登錄。 若失敗，應用程式重新啟動時，就會重新驗證。



<!--
### Related Information {#related}


- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note)](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->