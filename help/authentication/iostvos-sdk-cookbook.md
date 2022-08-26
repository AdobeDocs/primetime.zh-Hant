---
title: iOS/電視OS烹飪書
description: iOS/電視OS烹飪書
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '2434'
ht-degree: 0%

---


# iOS/電視OS SDK指南 {#iostvos-sdk-cookbook}

- [導言](#intro)
- [權利流](#entitlement)
- [相關資訊](#related)

>[!NOTE]
>
>**通知**:此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>


## 導言 {#intro}

本文檔介紹程式設計師的高級應用程式可以通過iOS/tvOS AccessEnabler庫公開的API實施的權利工作流。

 

iOS/tvOS的Adobe Primetime認證權限解決方案最終分為兩個域：

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
1. AppleSSO流動：推廣AppleVSA框架

AccessEnabler的網路活動發生在其自己的線程中，因此UI線程從不被阻止。 因此，兩個應用域之間的雙向通信通道必須遵循完全非同步模式：

- UI應用層通過AccessEnabler庫公開的API調用向AccessEnabler域發送消息。
- AccessEnabler通過AccessEnabler協定中包含的回調方法對UI層作出響應，UI層在AccessEnabler庫中註冊了該回調方法。

 

## 配置訪問者ID {#visitorIDSetup}

配置 [Marketing Cloud訪問者ID](https://marketing.adobe.com/resources/help/en_US/mcvid/) 從分析的角度來看，價值非常重要。 一旦設定了visitorID值，SDK將隨每個網路呼叫一起發送此資訊，而Adobe Primetime身份驗證伺服器將收集此資訊。 將來，您將能夠將來自Adobe Primetime身份驗證服務的分析與來自其他應用程式或網站的任何其他分析報告相關聯。 有關如何設定visitorID的資訊可以找到 [這裡](#setOptions)。

 

## 權利流 {#entitlement}

答：  [先決條件](#prereqs) </br>
B  [啟動流](#startup_flow) </br>
C.  [使用AppleSSO的驗證流](#authn_flow_wo_applesso)  </br>
D  [在iOS上使用AppleSSO的身份驗證流](#authn_flow_with_applesso) </br>
E.  [在tvOS上使用AppleSSO的驗證流](#authn_flow_with_applesso_tvOS) </br>
F.  [授權流](#authz_flow) </br>
G.  [查看媒體流](#media_flow) </br>
H  [沒有AppleSSO的註銷流](#logout_flow_wo_AppleSSO) </br>
我。  [使用AppleSSO註銷流](#logout_flow_with_AppleSSO) </br>

 

### 答：先決條件 {#prereqs}

1. 建立回調函式：
   - `setRequestorComplete()` </br>
      - 觸發者 [setRequestor()](#$setReq)，返回成功或失敗。 </br>
      - 成功表示您可以繼續權利調用。
   - [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      - 觸發者 [`getAuthentication()`](#$getAuthN) 僅當用戶尚未選擇提供程式(MVPD)且尚未驗證時，才可使用。 </br>
      - 的 `mvpds` 參數是用戶可用的提供程式陣列。
   - `setAuthenticationStatus(status, errorcode)` </br>
      - 觸發者 `checkAuthentication()` 每次。  </br>
      - 觸發者 [`getAuthentication()`](#$getAuthN) 僅當用戶已經過身份驗證並已選擇提供程式時。 </br>
      - 返回的狀態是成功或失敗，錯誤代碼描述失敗的類型。
   - [`navigateToUrl(url)`](#$nav2url) </br>
      - 觸發者 [`getAuthentication()`](#$getAuthN) 在用戶選擇MVPD後。  的 `url` 參數提供MVPD登錄頁的位置。
   - `sendTrackingData(event, data)` </br>
      - 觸發者 `checkAuthentication()`。 [`getAuthentication()`](#$getAuthN)。 `checkAuthorization()`。 [`getAuthorization()`](#$getAuthZ)。 `setSelectedProvider()`。
      - 的 `event` 參數指示發生了哪些權利事件；這樣 `data` 參數是與事件相關的值清單。 
   - `setToken(token, resource)`

      - 觸發者 [checkAuthorization()](#checkAuthZ) 和 [getAuthorization()](#$getAuthZ) 在成功授權查看資源後。
      - 的 `token` 參數是短壽命的媒體令牌；這樣 `resource` 參數是用戶有權查看的內容。
   - `tokenRequestFailed(resource, code, description)` </br>
      - 觸發者 [checkAuthorization()](#checkAuthZ) 和 [getAuthorization()](#$getAuthZ) 授權失敗。
      - 的 `resource` 參數是用戶嘗試查看的內容；這樣 `code` 參數是錯誤代碼，指示出現了哪種類型的故障；這樣 `description` 參數描述與錯誤代碼相關的錯誤。
   - `selectedProvider(mvpd)` </br>
      - 觸發者 [`getSelectedProvider()`](#getSelProv)。
      - 的 `mvpd` 參數提供有關用戶選擇的提供程式的資訊。
   - `setMetadataStatus(metadata, key, arguments)`
      - 觸發者 `getMetadata().`
      - 的 `metadata` 參數提供您請求的特定資料；這樣
         `key` 參數是 [getMetadata()](#getMeta)
請求；和 
`arguments` 參數是傳遞給的同一字典 [getMetadata()](#getMeta)。
   - [&#39;preauthoredResources(authorizedResources)&#39;](#preauthResources)

      - 觸發者 [`checkPreauthorizedResources()`](#checkPreauth)。
      - 的 `authorizedResources` 參數顯示用戶有權查看的資源。
   - [「presentTvProviderDialog(viewController)」](#presentTvDialog)
      - 觸發者 [getAuthentication()](#getAuthN) 當當前請求者至少支援具有SSO支援的MVPD時。
      - viewController參數是AppleSSO對話框，需要顯示在主視圖控制器上。
   - [&#39;dismisdTvProviderDialog(viewController)&#39;](#dismissTvDialog)
      - 由用戶操作觸發(通過從「AppleSSO」對話框中選擇「取消」或「其他電視提供商」)。
      - viewController參數是AppleSSO對話框，需要從主視圖控制器中刪除。












</br>


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOS_flows\(1\)。png)\
 

### B啟動流 {#startup_flow}

1. 啟動高級應用程式。</br>
1. 啟動Adobe Primetime身份驗證 </br></br>
a.呼叫 [`init`](#$init) 建立Adobe Primetime身份驗證AccessEnabler的單個實例。
   - **依賴關係：** Adobe Primetime本機iOS/tvOS庫驗證(AccessEnabler)
   b.呼叫 `setRequestor()` 確定程式設計師的身份；程式設計師 `requestorID` 和（可選）Adobe Primetime驗證端點的陣列。 對於tvOS，您還需要提供公鑰和秘密。 請參閱 [無客戶端文檔](#create_dev) 的雙曲餘切值。
   - **依賴關係：** 有效的Adobe Primetime驗證請求者ID\
      (與您的Adobe Primetime身份驗證客戶經理合作安排。)
   - **觸發器：**

      [setRequestorComplete()](#$setReqComplete) 回調
   >[!NOTE]
   >
   > **注：** 在完全建立請求者身份之前，無法完成任何權利請求。 這實際上意味著 [`setRequestor()`](#$setReq)  仍在運行，所有後續的權利請求(例如， [`checkAuthentication()`](#checkAuthN) 中。

   您有兩個實施選項：一旦請求者標識資訊被發送到後端伺服器，UI應用層可以選擇以下兩種方法之一： </br>
   1. 等待觸發 [`setRequestorComplete()`](#setReqComplete) 回調（AccessEnabler委託的一部分）。  此選項最確定地 [`setRequestor()`](#$setReq) 已完成，因此建議用於大多數實施。
   1. 繼續，而不等待觸發 [`setRequestorComplete()`](#setReqComplete) 回調，並開始發出權利請求。 這些調用(checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、logout)由AccessEnabler庫排隊，該庫將在AccessEnabler之後進行實際的網路調用 [`setRequestor()`](#$setReq)。 例如，如果網路連接不穩定，則有時可能會中斷此選項。



1. 呼叫 `checkAuthentication()` 檢查現有驗證而不啟動完整驗證流。  如果此調用成功，則可以直接進入授權流。  否則，繼續驗證流。

   - **依賴關係：** 成功調用 [setRequestor()](#$setReq)
（此依賴關係也適用於所有後續調用）。

   - **觸發器：** [setAuthenticationStatus()](#$setAuthNStatus) 回調

 

### C.沒有AppleSSO的驗證流 {#authn_flow_wo_applesso}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流，或獲得用戶已經驗證的確認。 \
   **觸發器：**  

   - 的 [setAuthenticationStatus()](#$setAuthNStatus) 回調，如果用戶已經經過身份驗證。  在這種情況下，請直接轉到 [授權流](#authz_flow)。
   - 的 [displayProviderDialog()](#$dispProvDialog) 回調，如果用戶尚未通過身份驗證。  

1. 向用戶顯示發送到的提供程式清單
   [`displayProviderDialog()`](#dispProvDialog)。

1. 用戶選擇提供程式後，從 `navigateToUrl:` 或 `navigateToUrl:useSVC:` 回調並開啟 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器，並將該控制器定向到URL。   

1. 通過 `UIWebView/WKWebView` 或 `SFSafariViewController` 在上一步中實例化後，用戶將登陸MVPD的登錄頁並輸入登錄憑據。 在控制器內進行多個重定向操作。</br></br>
   **注釋**  — 此時，用戶有機會取消驗證流。 如果發生這種情況，則您的UI層負責通過調用將此事件通知AccessEnabler [setSelectedProvider()](#setSelProv) 與 `null` 的雙曲餘切值。 這允許AccessEnabler清除其內部狀態並重置身份驗證流。

1. 用戶成功登錄後，應用層將檢測特定自定義URL的載入。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為驗證流程已完成並且關閉 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器。 以防 `SFSafariViewController `控制器需要使用由 **`application's custom scheme`** (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自定義URL由 **`ADOBEPASS_REDIRECT_URL`** 常數(即 `adobepass://ios.app`)。

1. 關閉UIWebView/WKWebView或SFSafariViewController控制器並調用AccessEnabler `handleExternalURL:url `API方法`,` 指示AccessEnabler從後端伺服器檢索身份驗證令牌。 

1. [可選] 呼叫    [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。  的 `resources` 參數是與用戶的驗證令牌關聯的受保護資源的陣列。  從用戶的MVPD獲取的授權資訊的一個用途是裝飾您的UI（例如，受保護內容旁邊的鎖定/解鎖符號）。

   - **觸發器：** [`preauthorizedResources()`](#preauthResources) 回調
   - **執行點：** 完成身份驗證流程後

1. 如果驗證成功，請繼續到授權流。

 

### D在iOS上使用AppleSSO的身份驗證流 {#authn_flow_with_applesso}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流，或獲得用戶已經驗證的確認。 \
   **觸發器：**  

   - 的 [presentTvProviderDialog()](#presentTvDialog) 回調，如果用戶未通過身份驗證，且當前請求者至少在支援SSO的MVPD上具有。 如果沒有MVPD支援SSO，則將使用經典身份驗證流。

1. 用戶選擇提供程式後，AccessEnabler庫將獲取一個驗證令牌，該令牌包含AppleVSA框架提供的資訊。

1. 的 [setAuthenticationsStatus()](#setAuthNStatus) 將觸發回調。 此時應使用AppleSSO對用戶進行身份驗證。

1. [可選] 呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。 的 `resources` 參數是與用戶的驗證令牌關聯的受保護資源的陣列。  從用戶的MVPD獲取的授權資訊的一個用途是裝飾您的UI（例如，受保護內容旁邊的鎖定/解鎖符號）。

   - **觸發器：** [`preauthorizedResources()`](#preauthResources) 回調
   - **執行點：** 完成身份驗證流程後

1. 如果驗證成功，請繼續到授權流。

 

### E.在tvOS上使用AppleSSO的驗證流 {#authn_flow_with_applesso_tvOS}

1. 呼叫 [`getAuthentication()`](#$getAuthN) 啟動驗證流，或獲得用戶已經驗證的確認。 \
   **觸發器：**  
   - 的 [`presentTvProviderDialog()`](#presentTvDialog) 回調，如果用戶未通過身份驗證，且當前請求者至少在支援SSO的MVPD上具有。 如果沒有MVPD支援SSO，則將使用經典身份驗證流。

1. 用戶選擇提供程式後， [`status()`](#status_callback_implementation) 將調用回調。 將提供註冊代碼，AccessEnabler庫將開始輪詢伺服器以獲得成功的第二螢幕身份驗證。

1. 如果提供的註冊代碼用於在第二個螢幕上成功驗證，則 [`setAuthenticatiosStatus()`](#setAuthNStatus) 將觸發回調。 此時應使用AppleSSO對用戶進行身份驗證。
1. [可選] 呼叫 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 檢查用戶有權查看的資源。 的 `resources` 參數是與用戶的驗證令牌關聯的受保護資源的陣列。  從用戶的MVPD獲取的授權資訊的一個用途是裝飾您的UI（例如，受保護內容旁邊的鎖定/解鎖符號）。
   - **觸發器：** [`preauthorizedResources()`](#preauthResources) 回調
   - **執行點：** 完成身份驗證流程後
1. 如果驗證成功，請繼續到授權流。

 

### F.授權流 {#authz_flow}

1. 呼叫 [getAuthorization()](#$getAuthZ) 啟動授權流。
   - **依賴關係：** 與MVPD一致的有效資源ID。
   - 資源ID應與任何其他設備或平台上使用的ID相同，並且在MVPD上將相同。 有關資源ID的資訊，請參見 [確定受保護的資源](https://tve.helpdocsonline.com/4-2-2-3)

1. 驗證身份驗證和授權。

   - 如果 [getAuthorization()](#$getAuthZ) 呼叫成功：用戶具有有效的AuthN和AuthZ令牌（用戶已通過身份驗證並被授權監視請求的媒體）。
   - 如果 [getAuthorization()](#$getAuthZ) 失敗：檢查拋出的異常以確定其類型（AuthN、AuthZ或其他）:
      - 如果是驗證(AuthN)錯誤，則重新啟動驗證流。
      - 如果是授權(AuthZ)錯誤，則用戶無權監視請求的媒體，應向用戶顯示某種錯誤消息。
      - 如果存在其他類型的錯誤（連接錯誤、網路錯誤等） 然後向用戶顯示相應的錯誤消息。

1. 驗證短媒體令牌。\
   使用Adobe Primetime驗證媒體令牌驗證器庫驗證從 [getAuthorization()](#$getAuthZ) 以上呼叫：

   - 如果驗證成功：為用戶播放請求的媒體。
   - 如果驗證失敗：AuthZ令牌無效，應拒絕媒體請求，並應向用戶顯示錯誤消息。


1. 返回到正常應用程式流。

 

### G.查看媒體流 {#media_flow}

1. 用戶選擇要查看的媒體。
1. 介質是否受到保護？  您的應用程式將檢查所選介質是否受保護：
   - 如果選定的介質受保護，應用程式將啟動 [授權流](#authz_flow) 上。
   - 如果選定的介質未受保護，則播放用戶的介質。

 

### H沒有AppleSSO的註銷流 {#logout_flow_wo_AppleSSO}

1. 呼叫 [`logout()`](#$logout) 將用戶註銷。 AccessEnabler將清除所有快取值和令牌。 清除快取後，AccessEnabler會調用伺服器來清除伺服器端會話。 請注意，由於伺服器調用可能導致SAML重定向到IdP（這允許在IdP端進行會話清理），因此此調用必須遵循所有重定向。 因此，必須在UIWebView/WKWebView或SFSafariViewController控制器內處理此調用。

   - a.遵循與身份驗證工作流相同的模式，AccessEnabler域通過 `navigateToUrl:` 或 `navigateToUrl:useSVC:` 回調，建立UIWebView/WKWebView或SFSafariViewController控制器，並指示載入回調中提供的URL `url` 的下界。 這是後端伺服器上註銷終結點的URL。

   - b.您的應用程式必須監視 `UIWebView/WKWebView or SFSafariViewController` 控制器，並檢測當它載入特定自定義URL時，它經過多次重定向。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為註銷流程已完成並且關閉 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器。 當控制器載入此特定自定義URL時，您的應用程式必須關閉 `UIWebView/WKWebView or SFSafariViewController` 控制器並調用AccessEnabler `handleExternalURL:url`API方法。 以防 `SFSafariViewController`控制器需要使用由 **`application's custom scheme`** (例如 `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自定義URL由 **`ADOBEPASS_REDIRECT_URL`**  常數(即 `adobepass://ios.app`)。

      >[!NOTE]
      >
      > **注：** 註銷流與驗證流不同，因為用戶不需要以任何方式與UIWebView/WKWebView或SFSafariViewController交互。 UI應用層使用UIWebView/WKWebView或SFSafariViewController來確保遵循所有重定向。 因此，在註銷過程中，可能（並建議）使控制器不可見（即隱藏）。


### 我。使用AppleSSO註銷流 {#logout_flow_with_AppleSSO}

1. 呼叫 [`logout()`](#$logout) 將用戶註銷。 
1. 的 [狀態()](#status_callback_implementation) 將使用VSA203調用回調。
1. 還應指示用戶從系統設定登錄。 如果失敗，將在應用程式重新啟動時導致重新驗證。

</br>

### 相關資訊 {#related}

<!---
- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note) ](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->
