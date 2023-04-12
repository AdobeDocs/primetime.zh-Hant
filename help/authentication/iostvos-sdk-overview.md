---
title: iOS/tvOS SDK概述
description: iOS/tvOS SDK概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 0%

---


# iOS/tvOS SDK概述 {#iostvos-sdk-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


</br>


## 簡介 {#intro}

iOS AccessEnabler是Objective C iOS/tvOS資料庫，可讓行動應用程式使用Adobe Primetime驗證以取得TV Everywhere的權益服務。 實作包含 *AccessEnabler* 定義權利API的介面，以及 *EntitlementDelegate* 和 *[EntitlementStatus](#ios%20entitlement%20status)* 說明程式庫觸發之回呼的通訊協定。 該介面與協定以一個通用名稱引用：AccessEnabler庫。

## iOS和tvOS需求 {#reqs}

如需iOS和tvOS平台及Primetime驗證的目前技術需求，請參閱 [平台/裝置/工具需求](#ios)，並參閱SDK下載內含的發行說明。 在本頁的其餘部分中，您將看到適用於特定SDK版本及更高版本的注意事項更改。 例如，下列是關於1.7.5 SDK的合法附註：

## 了解原生用戶端工作流程 {#flows}

原生用戶端工作流程通常與瀏覽器型Primetime驗證用戶端的工作流程相同或非常類似。 但是，有一些例外，如下所述。

- [初始化後工作流](#post-init)
- [一般初始驗證工作流程](#generic)
- [登出工作流程](#logout)


### 初始化後工作流 {#post-init}

AccessEnabler支援的所有權利工作流假定您以前已調用 [`setRequestor()`](#setReq) 來確認你的身份。 您發出此呼叫時，通常只會在應用程式的初始化/設定階段期間提供要求者ID一次。


使用iOS原生用戶端，在您初次呼叫 [`setRequestor()`](#setReq)，您可以選擇如何繼續：

- 您可以立即開始進行權限呼叫，並視需要允許他們以靜默方式佇列。

- 您可以收到 [`setRequestor()`](#setReq) 執行 [`setRequestorComplete()`](#setReqComplete) 回呼。

- 您可以同時執行上述兩項操作。

您可以選擇讓應用程式等候通知，告知其成功 [`setRequestor()`](#setReq) 或者讓它依賴AccessEnabler的呼叫隊列機制。 由於所有後續的授權和驗證請求都需要請求者ID和相關的配置資訊，因此， [`setRequestor()`](#setReq) 方法會有效封鎖所有驗證和授權API呼叫，直到初始化完成為止。

 

### 一般初始驗證工作流程 {#generic}

此工作流程的用途是使用其MVPD登入使用者。 成功登入後，後端伺服器會向使用者發出驗證Token。 雖然驗證通常是在授權過程中完成的，但以下說明如何隔離進行驗證，並且不包括任何授權步驟。

請注意，雖然本機用戶端的此工作流程與一般的瀏覽器式驗證工作流程不同，但原生用戶端和瀏覽器式用戶端的步驟1至5都相同。

1. 您的應用程式以對AccessEnabler的調用啟動身份驗證工作流 `getAuthentication() `API方法，會檢查是否有有效的快取驗證Token。
1. 如果用戶當前已通過驗證，則AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 回呼函式，傳遞表示成功的驗證狀態，並結束流程。
1. 如果用戶當前未被驗證，則AccessEnabler通過確定用戶的上次驗證嘗試是否在給定MVPD下成功來繼續驗證流。 如果已快取MVPD ID，且 `canAuthenticate` 標幟為true，或已使用 [`setSelectedProvider()`](#setSelProv)，系統不會以MVPD選取對話方塊提示使用者。 驗證流程會繼續使用MVPD的快取值（亦即上次成功驗證期間使用的相同MVPD）。 系統會對後端伺服器發出網路呼叫，並將使用者重新導向至MVPD登入頁面（下方的步驟6）。
1. 如果未快取任何MVPD ID，且未使用 [`setSelectedProvider()`](#setSelProv) 或 `canAuthenticate` 標幟設為false, [`displayProviderDialog()`](#dispProvDialog) 呼叫回呼。 此回呼會指示您的應用程式建立UI，為使用者提供要選擇的MVPD清單。 提供MVPD物件的陣列，其中包含您建立MVPD選取器的必要資訊。 每個MVPD物件都描述MVPD實體，並包含MVPD的ID（例如XFINITY、AT\&amp;T等）等資訊 和可找到MVPD標誌的URL。
1. 選擇特定MVPD後，您的應用程式必須通知AccessEnabler用戶的選擇。 一旦用戶選擇了所需的MVPD，您就通過對 [`setSelectedProvider()`](#setSelProv) 方法。
1. iOS AccessEnabler將調用 `navigateToUrl:` 回呼或 `navigateToUrl:useSVC:` 回撥，將使用者重新導向至MVPD登入頁面。 通過觸發任一個，AccessEnabler會向您的應用程式請求建立 `UIWebView/WKWebView or SFSafariViewController` 控制器和，以載入回呼中提供的URL `url` 參數。 這是後端伺服器上驗證端點的URL。 對於tvOS AccessEnabler, [status()](#status_callback_implementation) 使用呼叫 `statusDictionary` 參數和第二個螢幕驗證的輪詢會立即開始。 此 `statusDictionary` 包含 `registration code` 需要用於第二個畫面驗證。 
1. 如果是iOS AccessEnabler，用戶將登陸MVPD的登錄頁，通過應用程式的介質輸入其憑據 `UIWebView/WKWebView or SFSafariViewController `控制器。 請注意，此傳輸期間會發生數個重新導向操作，而您的應用程式必須在多個重新導向操作期間監控控制器載入的URL。
1. 如果是iOS AccessEnabler，則 `UIWebView/WKWebView or SFSafariViewController` 控制器載入特定自定義URL，您的應用程式必須關閉控制器並調用AccessEnabler的 `handleExternalURL:url `API方法。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只能將其解讀為驗證流程已完成且關閉安全的信號 `UIWebView/WKWebView or SFSafariViewController` 控制器。 若您的應用程式需要使用 `SFSafariViewController `控制器由 `application's custom scheme` (例如： `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 `ADOBEPASS_REDIRECT_URL` 常數(即 `adobepass://ios.app`)。
1. 一旦您的應用程式關閉 `UIWebView/WKWebView or SFSafariViewController` 控制器和調用AccessEnabler的 `handleExternalURL:url `API方法，AccessEnabler會從後端伺服器擷取驗證Token，並通知您的應用程式驗證流程已完成。 AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態代碼為1的回呼表示成功。 如果執行這些步驟期間發生錯誤，則 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態碼為0時觸發回呼，表示驗證失敗，以及相應的錯誤碼。


>[!WARNING]
>
> 在AccessEnabler將控制權讓給您的應用程式的步驟中（即當顯示提供程式選擇對話框時，或當顯示UIWebView/WKWebView或SFSafariViewController時），用戶有機會取消身份驗證流程。 在這些情況下，您的應用程式將負責向AccessEnabler通知此事件，並調用 [`setSelectedProvider()`](#setSelProv) API方法，傳遞null作為參數。 這使AccessEnabler有機會清除其內部狀態並重置身份驗證流。 在tvOS上，您可以使用相同的方法來取消驗證輪詢。


### 登出工作流程 {#logout}

對於本機用戶端，登出的處理方式與上述驗證程式類似。

1. 您的應用程式通過調用AccessEnabler的來啟動註銷工作流 `logout() `API方法。 登出是一系列HTTP重新導向操作的結果，因為使用者需要從Primetime驗證伺服器以及MVPD的伺服器登出。 因為此流無法通過AccessEnabler庫發出的簡單HTTP請求完成， `UIWebView/WKWebView or SFSafariViewController` 控制器需要具現化，才能遵循HTTP重新導向操作。

1. 採用與驗證流類似的模式。 iOS AccessEnabler觸發 `navigateToUrl:` callback或 `navigateToUrl:useSVC:` 建立 `UIWebView/WKWebView or SFSafariViewController` 控制器和，以載入回呼中提供的URL `url` 參數。 這是後端伺服器上登出端點的URL。 對於tvOS AccessEnabler , `navigateToUrl:` callback或 `navigateToUrl:useSVC:` 呼叫回呼。

1. 當它經過數個重新導向時，您的應用程式必須監控 `UIWebView/WKWebView or SFSafariViewController `controller和偵測載入特定自訂URL的時機。 請注意，此特定自訂URL實際上無效，且並非供控制器實際載入。 您的應用程式只能將它解釋為註銷流程已完成且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉控制器並調用AccessEnabler的 `handleExternalURL:url `API方法。 若您的應用程式需要使用 `SFSafariViewController `控制器由 `application's custom scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自訂URL會由 ` ADOBEPASS_REDIRECT_URL  `常數(即 `adobepass://ios.app`)。

1. 最後，AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態代碼為0的回呼，表示登出流程成功。

註銷流與驗證流不同，因為用戶不需要與 `UIWebView/WKWebView or SFSafariViewController`  控制者。 因此，Adobe建議您在註銷過程中隱藏控制項（即隱藏）。

## 代號 {#tokens}

- [定義與使用](#definitions)
- [快取准則](#caching)
- [持久性](#persistence)
- [格式](#format)
- [設備綁定](#device_binding)


### 定義與使用 {#definitions}

Primetime驗證權限解決方案的核心是產生特定資料片段（代號），這些資料片段（代號）是Primetime驗證在成功完成驗證和授權工作流程後所產生。 這些代號會儲存在用戶端的iOS裝置上。

 

代號的有效期有限；到期後，需透過重新啟動驗證和/或授權工作流程來重新核發權杖。

 

在權限工作流程期間發出的代號有三種：

- **驗證Token:** 用戶驗證工作流的最終結果將是驗證GUID,AccessEnabler可以使用它代表用戶進行授權查詢。 此驗證GUID會有與使用者驗證工作階段本身不同的相關存留時間(TTL)值。 將驗證GUID綁定到啟動驗證請求的設備，將生成驗證令牌。
- **授權Token:** 授予對由唯一resourceID標識的特定受保護資源的訪問權。 它包含授權方發出的授權授權，以及原始的resourceID。 此資訊會系結至起始請求的裝置。
- **短期媒體代號：** AccessEnabler通過返回短期媒體令牌來授予對給定資源的托管應用程式的訪問權限。 該令牌基於先前為該特定資源獲取的授權令牌而生成。 此外，此代號未系結至裝置，且相關的生命週期會明顯縮短(預設值：5分鐘)。

成功驗證和授權後，Primetime驗證會發出驗證、授權和短期媒體權杖。 這些代號應在使用者裝置上快取，並在其相關聯的有效期內使用。

 

### 快取准則 {#caching}

- 驗證Token
- 授權Token
- 短期媒體代號


#### 驗證Token

- **AccessEnabler 1.7:** 本SDK推出新的權杖儲存方法，可啟用多個程式設計人員 — MVPD貯體，因此可啟用多個驗證權杖。 現在，「每個請求者進行身份驗證」方案和正常身份驗證流程都使用相同的儲存佈局。 兩者的唯一差異在於驗證的執行方式：「每個請求者的身份驗證」包含一項新的改進（被動身份驗證），該改進使AccessEnabler能夠基於儲存器中的身份驗證令牌的存在（對於不同的程式設計師）執行後通道身份驗證。 使用者只需驗證一次，此工作階段即可用於取得其他應用程式中的驗證Token。 此後通道流會於 [`setRequestor()`](#setReq) 呼叫，對程式設計人員大都透明。 **然而，這裡有一個重要要求：程式設計師必須從主UI線程調用setRequestor()。**
- **AccessEnabler 1.6及更舊版本：** 在裝置上快取驗證Token的方式取決於&#x200B;**每個請求者的身份驗證」** 與目前MVPD相關聯的標幟：

<!-- end list -->

1. 如果禁用「每個請求者的身份驗證」功能，則單個身份驗證令牌將儲存在全局貼上板中本地；此代號將在與目前MVPD整合的所有應用程式之間共用。
1. 如果啟用了「每個請求者的身份驗證」功能，則令牌將與執行身份驗證流的程式設計師顯式關聯（令牌將不儲存在全局貼上板中，而是儲存在僅對該程式設計師的應用程式可見的專用檔案中）。 更具體地說，將禁用不同應用程式之間的單一登錄(SSO);當切換到新應用時，用戶需要顯式地執行驗證流（前提是第二個應用的程式設計師與當前MVPD整合，並且本地快取中不存在該程式設計師的驗證令牌）。

 

#### 授權Token

在任何給定時刻，AccessEnabler都只會快取每個資源一個授權令牌。 可快取多個授權Token，但它們與不同資源相關聯。 每當頒發新授權令牌，且舊授權令牌已存在時， *相同的資源*，新代號會覆寫現有的快取值。

 

#### 媒體代號

完全不應快取短期媒體代號。 每次呼叫授權API時，應從伺服器擷取媒體代號，因為此API限制為一次性使用。

 

### 持久性 {#persistence}

Token必須在相同應用程式的連續執行中持續存在。 這表示一旦取得驗證和授權權杖，且使用者關閉應用程式，當使用者重新開啟應用程式時，應用程式即可使用相同的權杖。 此外，希望這些令牌能跨多個應用程式持續存在。 換言之，當使用者使用一個應用程式以特定身分提供者登入（成功取得驗證和授權權杖）後，相同的權杖可透過不同應用程式使用，且當透過相同身分提供者登入時，不再提示使用者提供憑證。 這類無縫驗證/授權工作流程讓Primetime驗證解決方案成為真正的TV-Everywhere實作。 

 

## iOS

iOS AccessEnabler程式庫可將代號資料儲存至「類似剪貼簿」的資料結構(稱為 *貼上板*. 此系統層級的共用資源提供可實施所需永久性代號使用案例的關鍵要素：

- **支援結構化儲存**  — 貼上板不僅是簡單的線性緩衝儲存結構。 它提供類似字典的儲存機制，允許根據用戶指定的鍵值進行資料索引。
- **支援使用基礎檔案系統的資料持久性**  — 貼上板結構的內容可標籤為永續性，在這種情況下，資料會儲存在裝置的內部記憶體中。

 

將特定令牌放入令牌快取後，AccessEnabler庫將在不同時間檢查其有效性。  有效的Token定義為：

- 代號的TTL尚未過期。
- 令牌的頒發者包含在允許的身分提供者清單中。

 

## tvOS

由於tvOS上的貼上板不可用，因此tvOS AccessEnabler庫使用NsUserDefaults作為儲存選項。 這解決了持續驗證和授權Token的問題，但儲存的資訊無法在不同應用程式之間共用。

 

**iOS 10貼上板變更 —** 從舊版iOS升級時，貼上板將被清除。 這表示所有應用程式都需要重新驗證。

 

**iOS 7貼上板變更 —** 由於iOS 7上貼上板的運作方式有所變更，在iOS 7上執行的應用程式之間的跨單一登入(Cross SSO)將會有限。 具有該應用程式的應用程式 `<Bundle Seed ID>`(也稱為 `<Team ID>`)將共用令牌，這意味著來自同一個程式設計師X的應用程式A1和A2將共用令牌，而應用程式A1（程式設計師X）和應用程式A3（程式設計師Y）將不共用令牌。 

- 如果捆綁種子ID/團隊ID是由相同布建設定檔產生，則2個應用程式之間相同。 如需詳細資訊，請前往此連結：
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- 無論使用的Primetime驗證SDK為何，iOS 7都會出現此「跨SSO」限制。 

請閱讀此技術說明，以了解有關在iOS 7和upper上配置SSO的更多資訊（此技術說明適用於Access Enabler v1.8和upper）: <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### 令牌儲存(AccessEnabler 1.7)

從AccessEnabler 1.7開始，令牌儲存器可以支援多個程式設計師 — MVPD組合，它依賴於可以容納多個身份驗證令牌的多級嵌套映射結構。 此新儲存不會以任何方式影響AccessEnabler公共API，並且不需要在程式設計師端進行更改。 以下範例說明此新功能：

1. 開啟App1（由Programmer1開發）。
1. 使用MVPD1（與Programmer1整合）進行驗證。
1. 暫停/關閉當前應用程式，並開啟App2（由程式設計師2開發）。
1. 假設Programmer2未與MVPD2整合；因此，使用者「不會」在App2中進行驗證。
1. 在App2中使用MVPD2（與Programmer2整合）進行驗證。
1. 切換回App1；用戶仍將通過Programmer1進行身份驗證。

在舊版AccessEnabler中，步驟6會將用戶顯示為未驗證，因為令牌儲存以前僅支援一個驗證令牌。

 

從一個程式設計師/ MVPD會話註銷將清除整個基礎儲存，包括設備上的所有其他程式設計師/ MVPD身份驗證令牌。 另一方面，取消驗證流程(叫用 [`setSelectedProvider(null)`](#setSelProv))不會清除基礎儲存，但只會影響當前程式設計師/ MVPD驗證嘗試（通過擦除當前程式設計師的MVPD）。

 

### 令牌導入程式(AccessEnabler 1.7)

AccessEnabler 1.7中包含的另一個與儲存相關的功能使從舊儲存區域導入身份驗證令牌成為可能。 此「令牌導入程式」有助於實現連續AccessEnabler版本之間的相容性，即使在升級儲存版本時，也能保持SSO狀態。 匯入工具會在 [`setRequestor()`](#setReq) 在以下兩種情況下運行（假設當前儲存中不存在當前程式設計師的有效驗證令牌）:

- 由特定程式設計師開發的1.7應用程式的首次安裝
- 將路徑升級到使用新儲存的未來AccessEnabler

導入操作對程式設計師是透明的，不需要在客戶端應用程式中進行任何代碼更改。

 

### 令牌清理器(AccessEnabler 1.7.5)

從AccessEnabler 1.7.5轉發，此服務運行於 [`setRequestor()`](#setReq)`. `這是由於iOS 7從WiFi MAC位址切換至IDFA以進行追蹤而開發。 消毒器可確保目前的儲存僅包含有效的驗證Token(根據先前使用MAC地址計算的裝置ID，在iOS7之前有效)。 令牌清理器刪除了所有無效令牌。 

 

在iOS 6上使用AccessEnabler 1.7.5應用程式，然後用戶更新到iOS 7時，令牌處理器服務最有用。 發生此情況時，iOS 6上取得的所有驗證Token現在都會無效(因為裝置ID演算法已從使用MAC位址變更為IDFA)。 消毒器會清除所有無效的代號，然後使用者會取消驗證。 

 

如果Token清理程式刪除無效的令牌，AccessEnabler將無法獲得授權，因為存在無效的驗證令牌。 這對最終用戶來說將很難調試，因為授權錯誤消息可能是模糊的，在確定導致問題的原因時沒有太大幫助。 

 

### 格式 {#format}

- [AuthN代號](#authn_token)
- [AuthZ代號](#authz_token)
- [短媒體代號](#short_token)
- [設備綁定](#device_binding)


請注意，此處僅包含AuthN和AuthZ代號格式，以供背景資訊使用。 這些代號的結構可隨時透過Primetime驗證進行變更。 程式設計師不需要知道AuthN和AuthZ代號的確切結構即可實作其應用程式，因為AuthN和AuthZ代號不會在本機裝置上公開。 短媒體代號 *is* 向程式設計師應用程式公開。

 

#### 驗證Token {#authn_token}

下列清單顯示驗證Token的格式：

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthenticationToken>
      <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
      <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>   
  </simpleAuthenticationToken>
```
 

#### 授權Token {#authz_token}

下列清單顯示授權Token的格式：

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthorizationToken>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
      <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>
  </simpleAuthorizationToken>
```
 

#### 短媒體代號 {#short_token}

以下清單顯示簡短媒體代號的格式。 此令牌會向程式設計師的應用程式公開。 在成功的授權過程結束時，它被分配給程式設計師的應用程式：

```
  <signatureInfo>signature<signatureInfo>
  <shortAuthorizationToken>
    <sessionGUID>session_guid</sessionGUID>
    <requestorID>requestor_id</requestorID>
    <resourceID>resource_id</resourceID>
    <ttl>ttl_in_ms</ttl>
    <issueTime>issue_time</issueTime>
    <mvpdId>mvpd_id</mvpdId>
    <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
  </shortAuthorizationToken>
```
 

### 設備綁定 {#device_binding}

在上方的XML清單中，記下標題為 `simpleTokenFingerprint`. 此標籤的用途是保留原生裝置ID個人化資訊。 AccessEnabler庫能夠獲取此類個性化資訊，並使其在權限調用期間可供Primetime身份驗證服務使用。 服務會使用此資訊並將其內嵌於實際的Token中，借此有效將Token系結至特定裝置。 其最終目標是讓代號不可跨裝置轉讓。

 

由於這顯然是與安全相關的功能，因此從安全性角度來看，此資訊本身就是「敏感」的。 因此，需要保護這些資訊不受篡改和竊聽。 通過HTTPS協定發送身份驗證/授權請求來解決竊聽問題。 通過數字簽名設備標識資訊來處理篡改保護。 AccessEnabler庫根據設備提供的資訊計算設備ID，然後將設備ID「在清除中」作為請求參數發送到Primetime驗證伺服器。 Primetime驗證伺服器使用Adobe的私密金鑰對裝置ID進行數位簽署，並將其新增至傳回至AccessEnabler的驗證Token。 因此，裝置ID與驗證Token系結。 在授權流程中，AccessEnabler會再次以清除方式發送設備ID以及驗證令牌。 驗證程式失敗會自動導致驗證/授權工作流程失敗。 Primetime驗證伺服器會將私密金鑰套用至裝置ID，並與驗證Token中的值比較。 如果兩者不相符，則授權流程會失敗。

 

**AccessEnabler 1.7.5中設備綁定的注意事項：** 從AccessEnabler 1.7.5開始，計算設備ID的方式發生了變化，為iOS設備提供個性化資訊。 這項變更反映了iOS 7的變更：從iOS 7開始，Apple不再提供WiFi MAC位址作為追蹤選項，改用廣告商識別碼(IDFA)。 由於iOS 7上執行之應用程式的個人化資訊以IDFA為基礎，且該資訊內嵌於權限流程代號中，這表示此變更對使用者體驗可能會有許多不同的影響。 不同的可能效果取決於用戶從哪個版本升級到哪個版本的iOS，以及程式設計師從哪個版本升級的AccessEnabler。 有關此更改的詳細資訊，請參閱AccessEnabler SDK 1.7.5隨附的發行說明。

<!--
## Related Information {#related}


- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
