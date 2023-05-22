---
title: 程式設計師權利流
description: 程式設計師權利流
exl-id: b1c8623a-55da-4b7b-9827-73a9fe90ebac
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# 程式設計師權利流 {#prog-entitlement-flow}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview}

本文檔從程式設計師的角度描述了基本權利流。  有關此處介紹的基本TVE整合之外的功能和使用案例的資訊，請參見 [程式設計師使用案例](/help/authentication/programmer-use-cases.md)。

Adobe Primetime認證通過為雙方提供安全、一致的介面來調節程式設計師和MVPD之間的權利流。  在程式設計師方面，黃金時段身份驗證提供了兩種一般類型的權利介面：

1. AccessEnabler — 為可呈現網頁（如Web應用、智慧手機/平板電腦應用）的設備上的應用程式提供API庫的客戶端元件。
2. 無客戶端API — 用於無法呈現網頁（例如機頂盒、遊戲控制台、智慧電視）的設備的REST風格Web服務。 呈現網頁的要求來自MVPD要求用戶在MVPD的網站上進行身份驗證。

除了此處介紹的平台中性概述外，此處還提供了特定於客戶端的API概述：無客戶端API文檔。 AccessEnabler在受支援的平台(Web上的AS/JS、iOS上的Objective-C和Android上的Java)上以本機方式運行。 AccessEnabler API在支援的平台中是一致的。 所有不支援AccessEnabler的平台都使用相同的無客戶端API。

對於這兩種類型的介面，黃金時段身份驗證可安全地調整程式設計師應用和用戶MVPD之間的權利流：

![](assets/prog-entitlement-flow.png)


*圖：Adobe Primetime認證生態系統*

>[!IMPORTANT]
>
>上圖中注意，權利流程中有一部分不通過Adobe Primetime驗證伺服器：MVPD登錄。 用戶必須登錄到其MVPD的登錄頁。 由於這一要求，在無法呈現網頁的設備上，程式設計師應用程式必須指示用戶切換到能夠使用Web的設備以使用其MVPD登錄，然後返回原始設備以完成權利流的剩餘部分。

## 權利流 {#entitlement-flow}

有四個不同的子流構成了基本的權利流：

1. [啟動流](/help/authentication/entitlement-flow.md#startup)
1. [驗證流](/help/authentication/entitlement-flow.md#authentication)
1. [授權流](/help/authentication/entitlement-flow.md#authorization)
1. [註銷流](/help/authentication/entitlement-flow.md#logout)

在用戶最初訪問程式設計師站點時，權利流按上面的順序進行。 但是，在後續訪問中，根據驗證和授權令牌是否已過期，或根據查看策略，用戶可能只會通過其中的一個或兩個子流。

### 啟動流 {#startup}

建立程式設計師和設備的身份，執行初始化任務。 這是所有後續權利調用的先決條件。

**AccessEnabler**

* **`setRequestor()`**  — 使用AccessEnalber和擴展的Adobe Primetime身份驗證伺服器建立您的身份。 此呼叫是權利流其餘部分的前奏。 例如，在JavaScript中：

   ```JavaScript
     /* Define the requestor ID (Programmer/aggregator ID). */
       var requestorID = "sample_requestor_Id";
       ...
       // Callback indicating that the AccessEnabler swf has initialized
       function swfLoaded() {
           // AccessEnabler is loaded so we can use the API function it provides
           accessEnablerObject.setRequestor(requestorID); 
       ...
       }
   ```

**無客戶端API**

* **`\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode`**  — 根據平台的不同，在您的應用調用regcode之前可能需要完成先決任務。 查看 **無客戶端API文檔** 的雙曲餘切值。 例如，Xbox平台要求您在呼叫註冊碼之前完成規定的安全步驟。

### 驗證流 {#authentication}

成功的身份驗證將生成與設備和請求方綁定的AuthN令牌。 成功身份驗證是授權的先決條件。

**AccessEnabler**

* `checkAuthentication()`  — 檢查本地令牌快取中是否存在有效的快取身份驗證令牌，而不實際觸發完整身份驗證流。 這將觸發 `setAuthenticationStatus()` 回調函式。
* `getAuthentication()`  — 啟動完整驗證流。 如果成功，Adobe Primetime驗證將生成AuthN令牌，並在客戶端上快取該令牌。 用戶登錄到其選定的MVPD站點，視平台而定，這些站點顯示在iFrame、彈出窗口或webview中。 這將觸發displayProviderDialog()。

**無客戶端API**

* `<FQDN>/.../checkauthn` - Web服務版本 `checkAuthentication()` 上。
* `<FQDN>/.../config`  — 將MVPD清單返回到第2螢幕應用。
* `<FQDN>/.../authenticate`  — 從第2螢幕應用啟動身份驗證流，將用戶重定向到其選定的MVPD進行登錄。 如果成功，Adobe Primetime驗證將生成一個AuthN令牌並將其儲存在伺服器上，用戶將返回到其原始設備以完成權利流。

如果以下兩點為true，則AuthN令牌被視為有效：

* AuthN令牌未過期
* 與AuthN令牌關聯的MVPD位於當前請求者ID的允許MVPD清單中

#### 通用AccessEnabler初始身份驗證工作流 {#generic-ae-initial-authn-flow}

1. 您的應用啟動身份驗證工作流，並調用 `getAuthentication()`，用於檢查有效的快取身份驗證令牌。 此方法具有可選 `redirectURL` 參數；如果不為 `redirectURL`，成功驗證後，用戶將返回到初始化驗證的URL。
1. AccessEnabler可確定當前身份驗證狀態。 如果用戶當前已通過身份驗證，則AccessEnabler將調用 `setAuthenticationStatus()` 回調函式，傳遞一個驗證狀態，表示成功。
1. 如果用戶未經身份驗證，AccessEnabler將繼續身份驗證流程，方法是確定用戶上次使用給定MVPD進行身份驗證的嘗試是否成功。 如果快取MVPD ID，則 `canAuthenticate` 標誌為true，或使用 `setSelectedProvider()`,MVPD選擇對話框不會提示用戶。 驗證流繼續使用MVPD的快取值（即上次成功驗證期間使用的相同MVPD）。 對後端伺服器進行網路調用，並將用戶重定向到MVPD登錄頁。

1. 如果沒有快取MVPD ID，並且沒有使用 `setSelectedProvider()` 或 `canAuthenticate` 標誌設定為false, `displayProviderDialog()` 調用回調。 此回調將指示您的應用建立UI，該UI向用戶顯示要從中選擇的MVPD清單。 提供了MVPD對象陣列，其中包含構建MVPD選擇器所需的資訊。 每個MVPD對象都描述MVPD實體，並包含MVPD的ID和可找到MVPD徽標的URL等資訊。

1. 選擇MVPD後，您的應用必須通知AccessEnabler用戶的選擇。 對於非Flash客戶端，一旦用戶選擇了所需的MVPD，您就會通過對 `setSelectedProvider()` 的雙曲餘切值。 Flash客戶端而發送共用 `MVPDEvent` 類型&quot;`mvpdSelection`「 」，傳遞所選提供程式。

1. 當AccessEnabler獲知用戶的MVPD選擇時，會向後端伺服器進行網路調用，並將用戶重定向到MVPD登錄頁。

1. 在驗證工作流中，AccessEnabler與Adobe Primetime驗證和選定的MVPD通信，以徵求用戶憑據（用戶ID和密碼）並驗證其身份。 當某些MVPD重定向到其自己的站點進行登錄時，其他MVPD則要求您在iFrame中顯示其登錄頁。 您的頁面必須包括建立iFrame的回調，以防客戶選擇其中一個MVPD。<!-- For more information on creating a login iFrame, see  [Managing the Login IFrame](https://tve.helpdocsonline.com/managing-the-login-iframe)-->。

1. 用戶成功登錄後，AccessEnabler將檢索驗證令牌並通知您的應用驗證流已完成。 AccessEnabler將調用 `setAuthenticationStatus()` 狀態代碼為1的回調，表示成功。 如果執行這些步驟時出錯， `setAuthenticationStatus()` 回調被觸發，狀態代碼為0，表示身份驗證失敗，並且有相應的錯誤代碼。

>[!IMPORTANT]
>Comcast是目前唯一不提供徽標靜態URL的MVPD。 程式設計師應從 [XFINITY開發人員門戶](https://developers.xfinity.com/products/tv-everywhere)。

### 授權流 {#authorization}

授權是查看受保護內容的先決條件。 成功的授權會生成AuthZ令牌，以及為安全目的而提供給程式設計師應用的短生命週期媒體令牌。 請注意，要支援授權工作流，您以前必須執行了必要的請求程式設定並整合了 [媒體令牌驗證器](/help/authentication/media-token-verifier-int.md)。 完成這些操作後，您可以啟動授權。

當用戶請求訪問受保護的資源時，您的應用會啟動授權。 您會傳遞一個資源ID，指定所請求的資源（例如，頻道、集合等）。 你的應用首先檢查儲存的身份驗證令牌。 如果找不到，則啟動身份驗證過程。

**AccessEnabler**

* `checkAuthorization()`  — 在未啟動完全授權流的情況下檢查授權。 這通常用於更新程式設計師應用程式UI中顯示的狀態資訊。

* `getAuthorization()`  — 啟動完整授權流。

您提供以下回調函式來處理授權調用的結果：

* `setToken()`  — 如果以前身份驗證成功且授權成功，則AccessEnabler將調用 `setToken()` 回調函式，傳遞短命的媒體令牌，指示成功結束到Adobe Primetime身份驗證權限流。 (在允許用戶查看受保護內容之前，程式設計師應用使用媒體令牌驗證器檢查媒體令牌的有效性。

* `tokenRequestFailed()`  — 如果用戶未獲得請求資源的授權（或查詢因任何其他原因失敗），則AccessEnabler將調用此回調函式（加上您自己的錯誤報告函式），並傳遞有關失敗的詳細資訊。

**無客戶端API**

* `\<FQDN\>/.../authorize`  — 啟動完整授權流。

#### 通用AccessEnabler授權工作流 {#generic-ae-authr-wf}

1. 提供回調函式，該函式使用 `setReqestor()`。 成功下載AccessEnabler時調用此回調函式。

1. 呼叫 `getAuthorization()` 當用戶請求訪問受保護的資源時。 使用 `getAuthorization()`，傳遞指定所請求資源的資源ID（例如，頻道、插集等）。 AccessEnabler查找要隨授權請求傳遞的快取身份驗證令牌。 如果找不到，則啟動驗證流。
1. 提供回調函式以處理授權結果：

   * `setToken()`  — 如果授權成功或用戶以前已獲得授權，則Access Enabler將通過致電您 `setToken()` 回調函式，傳遞短時授權令牌。

   * `tokenRequestFailed()`  — 如果用戶未獲得請求資源的授權（或查詢因任何其他原因失敗）,AccessEnabler將調用您註冊的任何錯誤報告函式，加上 `tokenRequestFailed()` 回調，傳遞故障的詳細資訊。

### 註銷流 {#logout}

清除與當前用戶的權利流關聯的令牌和其他資料。

**AccessEnabler**

* `logout()`

**無客戶端API**

* `\<FQDN\>/.../logout`

## 瞭解AccessEnabler行為 {#ae-behavior}

所有AccessEnabler API調用都是非同步的（API引用中指出了一個例外）。 您可以任意調用API的次數，但無法強烈保證由調用觸發的操作將按與調用相同的順序完成。 (此操作的例外是當前Flash Player運行時；不是多線程，它將確保呼叫 *做* 按調用順序完成。)

為了區分響應和能夠將響應與呼叫配對，所有回叫都回復其輸入參數。 這包括 `setToken()` 和`tokenRequestFailed()`，而最終由 `checkAuthorization()`。 (對於 `checkAuthorization()` 回調，所用資源被回調。) 利用此功能，可以區分哪個響應與哪個呼叫對應。 要使用此功能，可以編碼如下內容：

```JavaScript
    for each (resource in ["TNT", "CNN", "TBS", "AdultSwim"] ) {
         ae.checkAuthorization(resource);
    }
    
    // Success callback
    function setToken(resource, token) {
         // Use "resource" to figure 
         // out which checkAuthorization
         // call triggered this response
    }
    
    // Old error callback
    function tokenRequestFailed(resource, error, details) {
         // use "resource" to figure
         // out in response to which
         // checkAuthorization call
         // this was triggered
    }
    
    // Error callback using new error api
    ae.bind("errorEvent',"errorHandler");
    
    function errorHandler(error) {
         if(error.resource) {        
              // Use error.resource to figure
              // which checkAuthorization call
              // triggered this response
         }
    }
```

### AE行為常見問題 {#ae-beh-faq}

**問題。 如果在第一次呼叫結束之前進行第二次AccessEnabler呼叫，會發生什麼情況？**

當第二呼叫執行（非同步通信）時，第一呼叫繼續執行。

**問題。 AccessEnabler是否支援最多的同時呼叫數？**

AccessEnabler代碼中未明確設定任何限制，因此您僅受可用系統資源以及MVPD容量的限制。

<!--

>[!MORELIKETHIS]
>
>*   [Programmer use cases](/help/authentication/programmer-use-cases.md)
>*   Error Reporting
>**Platform Cookbooks:**
>*   Clientless integration cookbook
>*   iOS Integration Cookbook
>*   Android Integration Cookbook
>*   JavaScript Integration Cookbook
>*   ActionScript Integration Cookbook
>*   Windows 8 Integration Cookbook
>*   AIR Native Extension Overview
-->
