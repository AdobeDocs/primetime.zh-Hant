---
title: iOS/tvOS SDK概述
description: iOS/tvOS SDK概述
exl-id: b02a6234-d763-46c0-bc69-9cfd65917a19
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 0%

---

# iOS/tvOS SDK概述 {#iostvos-sdk-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


</br>


## 導言 {#intro}

iOSAccessEnabler是一個目標CiOS/tvOS庫，它使移動應用能夠使用Adobe Primetime身份驗證來提供TV Everywhere的權利服務。 實施包括 *AccessEnabler* 定義權利API的介面，以及 *權利委託* 和 *[權利狀態](#ios%20entitlement%20status)* 描述庫觸發的回調的協定。 該介面與協定一起使用一個通用名稱：AccessEnabler庫。

## iOS和電視OS要求 {#reqs}

有關iOS和電視OS平台及黃金時段身份驗證的當前技術要求，請參閱 [平台/設備/工具要求](#ios)，並參考SDK下載附帶的發行說明。 在本頁的其餘部分中，您將看到一些章節，其中注釋了適用於特定SDK版本及更高版本的更改。 例如，以下是有關1.7.5 SDK的合法說明：

## 瞭解本機客戶端工作流 {#flows}

本機客戶端工作流通常與基於瀏覽器的黃金時段身份驗證客戶端的工作流相同或非常相似。 但是，有一些例外，如下所述。

- [初始化後工作流](#post-init)
- [通用初始驗證工作流](#generic)
- [註銷工作流](#logout)


### 初始化後工作流 {#post-init}

AccessEnabler支援的所有權利工作流都假定您以前調用過 [`setRequestor()`](#setReq) 來確認你的身份。 您進行此調用時僅提供一次請求者ID，通常在應用程式的初始化/設定階段。


與iOS本地客戶，在您初次呼叫 [`setRequestor()`](#setReq)，您可以選擇如何繼續：

- 您可以立即開始進行權利調用，並允許它們在需要時以靜默方式排隊。

- 您可以收到對 [`setRequestor()`](#setReq) 通過執行 [`setRequestorComplete()`](#setReqComplete) 回叫。

- 你可以做以上兩個。

您可以選擇讓您的應用程式等待通知其成功 [`setRequestor()`](#setReq) 或者讓它依賴AccessEnabler的呼叫隊列機制。 由於所有後續的授權和驗證請求都需要請求者ID和關聯的配置資訊， [`setRequestor()`](#setReq) 方法在初始化完成之前有效阻止所有驗證和授權API調用。

 

### 通用初始驗證工作流 {#generic}

此工作流的目的是使用其MVPD登錄用戶。 登錄成功後，後端伺服器向用戶發出身份驗證令牌。 雖然身份驗證通常作為授權過程的一部分完成，但下面介紹了身份驗證如何能夠獨立工作，並且不包括任何授權步驟。

請注意，雖然本機客戶端的此工作流與典型的基於瀏覽器的身份驗證工作流不同，但是對於本機客戶端和基於瀏覽器的客戶端，步驟1-5相同。

1. 您的應用程式通過調用AccessEnabler啟動身份驗證工作流 `getAuthentication() `API方法，它檢查有效的快取身份驗證令牌。
1. 如果用戶當前已通過身份驗證，則AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 回調函式，傳遞指示成功的驗證狀態，並結束流。
1. 如果用戶當前未經過身份驗證，則AccessEnabler會通過確定用戶上次使用給定MVPD進行身份驗證嘗試是否成功來繼續身份驗證流。 如果快取MVPD ID，則 `canAuthenticate` 標誌為true，或使用 [`setSelectedProvider()`](#setSelProv),MVPD選擇對話框不會提示用戶。 驗證流繼續使用MVPD的快取值（即上次成功驗證期間使用的相同MVPD）。 網路呼叫後端伺服器，並將用戶重定向到MVPD登錄頁（下面步驟6）。
1. 如果沒有快取MVPD ID，並且沒有使用 [`setSelectedProvider()`](#setSelProv) 或 `canAuthenticate` 標誌設定為false, [`displayProviderDialog()`](#dispProvDialog) 調用回調。 此回調將指示應用程式建立UI，該UI向用戶顯示要從中選擇的MVPD清單。 提供了MVPD對象陣列，其中包含構建MVPD選擇器所需的資訊。 每個MVPD對象都描述MVPD實體，並包含MVPD的ID（例如XFINITY、AT\&amp;T等）等資訊 以及找到MVPD徽標的URL。
1. 選擇特定MVPD後，您的應用程式必須通知AccessEnabler用戶的選擇。 一旦用戶選擇了所需的MVPD，您就會通過對 [`setSelectedProvider()`](#setSelProv) 的雙曲餘切值。
1. iOSAccessEnabler將 `navigateToUrl:` 回調 `navigateToUrl:useSVC:` 回調以將用戶重定向到MVPD登錄頁。 通過觸發其中一個，AccessEnabler會向您的應用程式發出請求，以建立 `UIWebView/WKWebView or SFSafariViewController` 控制器和載入回調中提供的URL `url` 的下界。 這是後端伺服器上驗證終結點的URL。 對於tvOS AccessEnabler, [狀態()](#status_callback_implementation) 使用調用 `statusDictionary` 參數，並立即啟動第二螢幕驗證的輪詢。 的 `statusDictionary` 包含 `registration code` 需要用於第二個螢幕驗證。 
1. 如果是iOSAccessEnabler，則用戶將登錄到MVPD的登錄頁面，通過應用程式的介質輸入其憑據 `UIWebView/WKWebView or SFSafariViewController `控制器。 請注意，在此傳輸過程中發生了多個重定向操作，並且您的應用程式必須監視控制器在多次重定向操作期間載入的URL。
1. 對於iOSAccessEnabler ，當 `UIWebView/WKWebView or SFSafariViewController` 控制器載入特定的自定義URL，您的應用程式必須關閉控制器並調用AccessEnabler `handleExternalURL:url `API方法。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為驗證流程已完成並且關閉 `UIWebView/WKWebView or SFSafariViewController` 控制器。 如果您的應用程式需要使用 `SFSafariViewController `控制器指定的自定義URL由 `application's custom scheme` (例如： `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自定義URL由 `ADOBEPASS_REDIRECT_URL` 常數(即 `adobepass://ios.app`)。
1. 一旦應用程式關閉 `UIWebView/WKWebView or SFSafariViewController` 控制器並調用AccessEnabler `handleExternalURL:url `API方法，AccessEnabler從後端伺服器檢索驗證令牌，並通知您的應用程式驗證流已完成。 AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態代碼為1的回調，表示成功。 如果執行這些步驟時出錯， [`setAuthenticationStatus()`](#setAuthNStatus) 回調被觸發，狀態代碼為0，表示身份驗證失敗，並且有相應的錯誤代碼。


>[!WARNING]
>
> 在AccessEnabler將控制權放棄給您的應用的步驟（即，當顯示提供程式選擇對話框時，或當顯示UIWebView/WKWebView或SFSafariViewController時）中，用戶有機會取消驗證流。 在這些情況下，您的應用負責向AccessEnabler通知此事件，並呼叫 [`setSelectedProvider()`](#setSelProv) API方法，將空值作為參數傳遞。 這使AccessEnabler有機會清除其內部狀態並重置身份驗證流。 在tvOS上，可以使用相同的方法取消驗證輪詢。


### 註銷工作流 {#logout}

對於本機客戶端，註銷的處理方式與上述驗證過程類似。

1. 您的應用程式通過調用AccessEnabler啟動註銷工作流 `logout() `API方法。 註銷是一系列HTTP重定向操作的結果，因為用戶需要從Mogine Authentication伺服器和MVPD伺服器註銷。 由於AccessEnabler庫發出的簡單HTTP請求無法完成此流，因此 `UIWebView/WKWebView or SFSafariViewController` 需要實例化控制器，以便能夠執行HTTP重定向操作。

1. 採用與認證流相似的模式。 iOSAccessEnabler觸發 `navigateToUrl:` 回調或 `navigateToUrl:useSVC:` 建立 `UIWebView/WKWebView or SFSafariViewController` 控制器和載入回調中提供的URL `url` 的下界。 這是後端伺服器上註銷終結點的URL。 對於tvOS AccessEnabler, `navigateToUrl:` 回調或 `navigateToUrl:useSVC:` 調用回調。

1. 在多次重定向時，您的應用程式必須監視 `UIWebView/WKWebView or SFSafariViewController `控制器並檢測載入特定自定義URL的時間。 請注意，此特定自定義URL實際上無效，並且不是供控制器實際載入的。 您的應用程式只能將其解釋為註銷流程已完成並且關閉控制器是安全的信號。 當控制器載入此特定自定義URL時，您的應用程式必須關閉控制器並調用AccessEnabler `handleExternalURL:url `API方法。 如果您的應用程式需要使用 `SFSafariViewController `控制器指定的自定義URL由 `application's custom scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否則此特定自定義URL由 ` ADOBEPASS_REDIRECT_URL  `常數(即 `adobepass://ios.app`)。

1. 最後， AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 回調，狀態代碼為0，表示註銷流成功。

註銷流與驗證流不同，因為用戶不需要與 `UIWebView/WKWebView or SFSafariViewController`  控制器。 因此，Adobe建議您使控制項不可見(即 隱藏)。

## 令牌 {#tokens}

- [定義和使用](#definitions)
- [快取准則](#caching)
- [持久性](#persistence)
- [格式](#format)
- [設備綁定](#device_binding)


### 定義和使用 {#definitions}

黃金時段身份驗證權利解決方案圍繞在成功完成身份驗證和授權工作流時黃金時段身份驗證生成的特定資料（令牌）的生成。 這些令牌儲存在客戶端的iOS設備上。

 

令牌的壽命有限；到期後，需要通過重新啟動驗證和/或授權工作流來重新頒發令牌。

 

在權利工作流期間發出的令牌有三種類型：

- **身份驗證令牌：** 用戶身份驗證工作流的最終結果將是身份驗證GUID,AccessEnabler可以使用該GUID代表用戶進行授權查詢。 此驗證GUID將具有與用戶的驗證會話本身不同的關聯生存時間(TTL)值。 通過將驗證GUID綁定到啟動驗證請求的設備，將生成驗證令牌。
- **授權令牌：** 授予對由唯一資源ID標識的特定受保護資源的訪問權限。 它包括由授權方簽發的授權授權以及原始資源ID。 此資訊綁定到啟動請求的設備。
- **短命的媒體令牌：** AccessEnabler通過返回短時間的媒體令牌，授予對給定資源的托管應用程式的訪問權限。 基於先前為該特定資源獲取的授權令牌生成此令牌。 此外，此令牌未綁定到設備，且關聯的壽命明顯縮短(預設值：5分鐘)。

在成功驗證和授權後，黃金時段驗證將發佈驗證、授權和短時間媒體令牌。 這些令牌應快取在用戶設備上，並在其關聯的生命週期內使用。

 

### 快取准則 {#caching}

- 驗證令牌
- 授權令牌
- 短期媒體令牌


#### 驗證令牌

- **AccessEnabler 1.7:** 此SDK引入了一種新的令牌儲存方法，它支援多個Programmer-MVPD儲存桶，從而支援多個驗證令牌。 現在，「每個請求者的身份驗證」方案和普通身份驗證流都使用相同的儲存佈局。 兩者的唯一區別在於身份驗證的執行方式：「每個請求者的身份驗證」包含一項新的改進（被動身份驗證），它使AccessEnabler能夠基於儲存器（對於其他程式設計師）中的身份驗證令牌的存在執行後通道身份驗證。 用戶只需驗證一次，此會話將用於獲取其他應用中的驗證令牌。 此後通道流發生於 [`setRequestor()`](#setReq) 並且對程式設計師大多是透明的。 **然而，這裡有一個重要要求：程式設計師MUST從主UI線程調用setRequestor()。**
- **AccessEnabler 1.6及更高版本：** 在設備上快取身份驗證令牌的方式取決於「 」**每個請求者的身份驗證」** 與當前MVPD關聯的標誌：

<!-- end list -->

1. 如果禁用「每個請求者的驗證」功能，則單個驗證令牌將本地儲存在全局貼上板中；此令牌將在與當前MVPD整合的所有應用程式之間共用。
1. 如果啟用了「每個請求者的身份驗證」功能，則一個令牌將與執行身份驗證流的程式設計師明確關聯（該令牌不會儲存在全局貼上板中，而是儲存在僅對該程式設計師的應用程式可見的專用檔案中）。 更具體地說，將禁用不同應用程式之間的單一登錄(SSO);用戶在切換到新應用時需要顯式執行驗證流（前提是第二個應用的程式設計師已與當前MVPD整合，並且本地快取中不存在該程式設計師的驗證令牌）。

 

#### 授權令牌

在任何給定時刻，AccessEnabler只快取每個資源一個授權令牌。 可以快取多個授權令牌，但它們與不同的資源相關聯。 只要頒發了新的授權令牌，並且舊的授權令牌已存在 *同一資源*，新令牌將覆蓋現有快取值。

 

#### 媒體令牌

根本不應快取短時間的媒體令牌。 每次調用授權API時，應從伺服器中檢索媒體令牌，因為它僅限於一次性使用。

 

### 持久性 {#persistence}

令牌需要在同一應用程式的連續運行中保持持久性。 這意味著一旦獲得了驗證和授權令牌並且用戶關閉了應用程式，當用戶重新開啟應用程式時，應用程式就可以使用相同的令牌。 此外，這些令牌在多個應用中是持久的。 換句話說，當用戶使用一個應用程式與特定身份提供程式登錄（成功獲取身份驗證和授權令牌）後，同一令牌可以通過不同的應用程式使用，並且當通過同一身份提供程式登錄時不再提示用戶提供憑據。 這種類型的無縫身份驗證/授權工作流使Mogfire身份驗證解決方案成為真正的TV-Everywhere實現。 

 

## iOS

iOSAccessEnabler庫通過將令牌資料儲存到稱為「剪貼簿」的資料結構中來解決跨應用程式資料共用問題 *貼上板*。 此系統級共用資源提供了關鍵要素，這些要素支援實現所需的持久令牌使用案例：

- **支援結構化儲存**  — 貼上板不僅是簡單的線性緩衝結構。 它提供了類似於字典的儲存機制，允許基於用戶指定的鍵值進行資料索引。
- **支援使用基礎檔案系統的資料持久性**  — 貼上板結構的內容可以標籤為持久，在這種情況下，資料將保存在設備的內部記憶體中。

 

將特定令牌放入令牌快取後，AccessEnabler庫將在不同時間檢查其有效性。  有效令牌定義為：

- 令牌的TTL未過期。
- 令牌的頒發者包含在允許的身份提供程式清單中。

 

## 電視作業系統

由於在tvOS上沒有貼上板，因此tvOS AccessEnabler庫將NsUserDefaults用作儲存選項。 這解決了驗證和授權令牌的永續問題，但儲存的資訊不能在不同的應用程式之間共用。

 

**iOS10貼上板更改 —** 從以前版本的iOS升級時，貼上板將被擦除。 這意味著所有應用程式都需要重新驗證。

 

**iOS7巴斯德板變更 —** 由於iOS7上貼上板的工作方式發生了變化，在iOS7上運行的應用程式之間的交叉SSO將有限。 具有該應用程式的應用程式 `<Bundle Seed ID>`(也稱為 `<Team ID>`)將共用令牌，即來自同一個程式設計師X的應用程式A1和A2將共用令牌，而應用程式A1（程式設計師X）和應用程式A3（程式設計師Y）將不共用令牌。 

- 如果捆綁種子ID/團隊ID是由同一預配配置檔案生成的，則兩個應用之間的捆綁種子ID相同。 在此連結上查找詳細資訊：
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- 此「跨SSO」限制將出現在iOS7中，而不管使用的黃金時段身份驗證SDK。 

請閱讀本技術說明，瞭解有關在iOS7和更高版本上配置SSO的詳細資訊（技術說明適用於Access Enabler v1.8和更高版本）: <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### 令牌儲存(AccessEnabler 1.7)

從AccessEnabler 1.7開始，令牌儲存可支援多個Programmer-MVPD組合，它依賴於一個可容納多個身份驗證令牌的多級嵌套映射結構。 此新儲存不會以任何方式影響AccessEnabler公共API，也不需要程式設計師方面的更改。 下面是一個示例，說明了此新功能：

1. 開啟App1（由程式設計師1開發）。
1. 通過MVPD1（與Programmer1整合）進行身份驗證。
1. 掛起/關閉當前應用程式，並開啟App2（由Programmer2開發）。
1. 假設程式設計師2未與MVPD2整合；因此，用戶將無法在App2中進行身份驗證。
1. 通過App2中的MVPD2（與Programmer2整合）進行身份驗證。
1. 切換回App1；用戶仍將通過Programmer1進行身份驗證。

在AccessEnabler的較舊版本中，步驟6會將用戶呈現為未經過身份驗證，因為以前令牌儲存僅支援一個身份驗證令牌。

 

從一個程式設計師/MVPD會話註銷將清除整個基礎儲存，包括設備上所有其他程式設計師/MVPD身份驗證令牌。 另一方面，取消驗證流(調用 [`setSelectedProvider(null)`](#setSelProv))不會清除底層儲存，但只會影響當前程式設計師/MVPD驗證嘗試（通過擦除當前程式設計師的MVPD）。

 

### 令牌導入程式(AccessEnabler 1.7)

AccessEnabler 1.7中包含的與儲存相關的另一個功能使可以從舊儲存區域導入身份驗證令牌。 此「令牌導入程式」有助於實現連續AccessEnabler版本之間的相容性，從而即使在升級儲存版本時也能保持SSO狀態。 導入程式在 [`setRequestor()`](#setReq) 並在以下兩種情況下運行（假定當前儲存中沒有當前程式設計師的有效身份驗證令牌）:

- 由特定程式設計師開發的1.7應用程式的首次安裝
- 將路徑升級到將來使用新儲存的AccessEnabler

導入操作對程式設計師是透明的，不需要在客戶端應用程式中更改任何代碼。

 

### 令牌清理程式(AccessEnabler 1.7.5)

從AccessEnabler 1.7.5轉發，此服務在 [`setRequestor()`](#setReq)`. `它是由於iOS7從WiFiMAC地址切換到IDFA進行跟蹤而開發的。 消毒器確保當前儲存僅包含有效的驗證令牌(根據設備ID有效，以前使用MAC地址計算，在iOS7之前)。 令牌清理程式將刪除所有無效令牌。 

 

在iOS6上使用AccessEnabler 1.7.5應用程式，然後用戶更新到iOS7時，令牌清理程式服務最有用。 如果發生這種情況，在iOS6上獲得的所有身份驗證令牌現在都將無效(因為設備ID算法從使用MAC地址更改為IDFA)。 清理程式將清除所有無效的令牌，然後用戶將被取消身份驗證。 

 

如果令牌清理程式不刪除無效的令牌，則AccessEnabler將無法獲取授權，因為存在無效的驗證令牌。 這對最終用戶來說將很難調試，因為授權錯誤消息可能很晦澀，在確定導致問題的原因方面也不會太有幫助。 

 

### 格式 {#format}

- [AuthN令牌](#authn_token)
- [AuthZ令牌](#authz_token)
- [短媒體令牌](#short_token)
- [設備綁定](#device_binding)


請注意，此處僅包含AuthN和AuthZ令牌的格式以獲取背景資訊。 這些令牌的結構可以隨時通過黃金時段認證來改變。 程式設計師不需要知道AuthN和AuthZ令牌的確切結構來實現其應用，因為本地設備上沒有公開AuthN和AuthZ令牌。 短媒體令牌 *是* 向程式設計師應用程式公開。

 

#### 驗證令牌 {#authn_token}

下面的清單顯示驗證令牌的格式：

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
 

#### 授權令牌 {#authz_token}

以下清單顯示授權令牌的格式：

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
 

#### 短媒體令牌 {#short_token}

以下清單顯示短媒體令牌的格式。 此令牌會暴露給程式設計師的應用程式。 在成功的權利流程結束時，它會被分配給程式設計師的應用程式：

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

在上面的XML清單中，請注意標題為 `simpleTokenFingerprint`。 此標籤的目的是保存本機設備ID個性化資訊。 AccessEnabler庫能夠獲取這種個性化資訊，並在權利調用期間將其提供給Mogine身份驗證服務。 服務將使用此資訊並將其嵌入到實際令牌中，從而有效地將令牌綁定到特定設備。 最終目標是使令牌不能跨設備傳輸。

 

由於這顯然是與安全相關的功能，因此從安全形度來看，此資訊具有內在的「敏感」性。 因此，需要保護這些資訊不受篡改和竊聽。 通過通過HTTPS協定發送驗證/授權請求來解決竊聽問題。 通過對設備標識資訊進行數字簽名來處理篡改保護。 AccessEnabler庫根據設備提供的資訊計算設備ID，然後將設備ID「在清除中」作為請求參數發送到黃金時段驗證伺服器。 Mighine身份驗證伺服器使用Adobe的私鑰對設備ID進行數字簽名，並將其添加到返回給AccessEnabler的身份驗證令牌中。 因此，設備ID與驗證令牌綁定。 在授權流程中， AccessEnabler再次以清除方式發送設備ID以及驗證令牌。 驗證過程失敗將自動導致驗證/授權工作流失敗。 黃金時段驗證伺服器將私鑰應用到設備ID，並將其與驗證令牌中的值進行比較。 如果它們不匹配，則該權利流將失敗。

 

**AccessEnabler 1.7.5中設備綁定的注意事項：** 從AccessEnabler 1.7.5開始，計算設備ID以為iOS設備提供個性化資訊的方式發生了變化。 這一變化反映了iOS7的變化：從iOS7號開始，Apple不再提供WiFiMAC地址作為跟蹤選項，而是提供其廣告商標識(IDFA)。 由於在iOS7上運行的應用的個性化資訊基於IDFA，並且該資訊嵌入到權利流令牌中，這意味著此更改對用戶體驗可能產生的多種不同影響。 不同的可能效果取決於用戶從哪個版本的iOS升級與程式設計師從哪個版本的AccessEnabler升級。 有關此更改的詳細資訊，請參閱AccessEnabler SDK 1.7.5附帶的發行說明。

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
