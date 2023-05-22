---
title: AmazonFireOS技術概述
description: AmazonFireOS技術概述
exl-id: 939683ee-0dd9-42ab-9fde-8686d2dc0cd0
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---

# AmazonFireOS技術概述 {#amazon-fireos-technical-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 導言 {#intro}

AmazonFireOS AccessEnabler由兩個元件表示：應用程式使用的AccessEnabler存根庫和系統級的Java Android庫，使移動應用能夠使用Adobe Primetime身份驗證來提供TV Everywhere的權利服務。 AmazonFireOS的Android實現包括定義權利API的AccessEnabler介面和描述庫觸發的回調的EntilementDelegate協定。 系統級AccessEnabler Android庫允許訪問Amazon服務，以便在平台級別啟用單一登錄。

## 瞭解本機客戶端工作流 {#native_client_workflows}

本機客戶端工作流通常與基於瀏覽器的黃金時段身份驗證客戶端的工作流相同或非常相似。 但是，有一些例外，如下所述。


### 初始化後工作流 {#post-init}

AccessEnabler支援的所有權利工作流都假定您以前調用過 [`setRequestor()`](#setRequestor) 來確認你的身份。 您進行此調用時僅提供一次請求者ID，通常在應用程式的初始化/設定階段。

在您初次呼叫Amazon FireOS後，使用本機客戶端 [`setRequestor()`](#setRequestor)，您可以選擇如何繼續：

- 您可以立即開始進行權利調用，並允許它們在需要時以靜默方式排隊。
- 或者，您可以收到對 [`setRequestor()`](#setRequestor) 通過實現setRequestorComplete()回調。
- 或者，兩者兼備。

是否等待通知成功與否由您決定 [`setRequestor()`](#setRequestor) 或依賴AccessEnabler的呼叫隊列機制。 由於所有後續的授權和驗證請求都需要請求者ID和關聯的配置資訊， [`setRequestor()`](#setRequestor) 方法在初始化完成之前有效阻止所有驗證和授權API調用。

### 通用初始驗證工作流 {#generic}

此工作流的目的是使用其MVPD登錄用戶。  登錄成功後，後端伺服器向用戶發出身份驗證令牌。 雖然身份驗證通常作為授權過程的一部分完成，但下面介紹了身份驗證如何能夠獨立工作，並且不包括任何授權步驟。

請注意，雖然以下本機客戶端工作流與典型的基於瀏覽器的驗證工作流不同，但對於本機客戶端和基於瀏覽器的客戶端，步驟1-5相同：

1. 您的頁面或播放器啟動身份驗證工作流時調用 [getAuthentication()](#getAuthN)，用於檢查有效的快取身份驗證令牌。 此方法具有可選 `redirectURL` 參數；如果不為 `redirectURL`，成功驗證後，用戶將返回到初始化驗證的URL。
1. AccessEnabler可確定當前身份驗證狀態。 如果用戶當前已通過身份驗證，則AccessEnabler將調用 `setAuthenticationStatus()` 回調函式，傳遞指示成功的驗證狀態（下面步驟7）。
1. 如果用戶未經身份驗證，AccessEnabler將繼續身份驗證流程，方法是確定用戶上次使用給定MVPD進行身份驗證的嘗試是否成功。 如果快取MVPD ID，則 `canAuthenticate` 標誌為true，或使用 [`setSelectedProvider()`](#setSelectedProvider),MVPD選擇對話框不會提示用戶。 驗證流繼續使用MVPD的快取值（即上次成功驗證期間使用的相同MVPD）。 網路呼叫後端伺服器，並將用戶重定向到MVPD登錄頁（下面步驟6）。
1. 如果沒有快取MVPD ID，並且沒有使用 [`setSelectedProvider()`](#setSelectedProvider) 或 `canAuthenticate` 標誌設定為false, [`displayProviderDialog()`](#displayProviderDialog) 調用回調。 此回調將指示您的頁面或播放器建立UI，該UI向用戶顯示要從中選擇的MVPD清單。 提供了MVPD對象陣列，其中包含構建MVPD選擇器所需的資訊。 每個MVPD對象都描述MVPD實體，並包含MVPD的ID（例如XFINITY、AT\&amp;T等）等資訊 以及找到MVPD徽標的URL。
1. 選擇特定MVPD後，您的頁面或播放器必須通知AccessEnabler用戶的選擇。 對於非Flash客戶端，一旦用戶選擇了所需的MVPD，您就會通過對 [`setSelectedProvider()`](#setSelectedProvider) 的雙曲餘切值。 Flash客戶端而發送共用 `MVPDEvent` 類型&quot;`mvpdSelection`「 」，傳遞所選提供程式。
1. 對於Amazon的申請， [`navigateToUrl()`](#navigagteToUrl) 將忽略回調。 Access Enabler庫便於訪問通用WebView控制項以驗證用戶。
1. 通過 `WebView`，用戶到達MVPD的登錄頁並輸入其憑據。 請注意，在此傳輸期間發生了多個重定向操作。 
1. 一旦WebView將完成身份驗證，它將關閉並通知AccessEnabler用戶已成功登錄，AccessEnabler將從後端伺服器檢索實際的身份驗證令牌。 AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態代碼為1的回調，表示成功。 如果執行這些步驟時出錯， [`setAuthenticationStatus()`](#setAuthNStatus) 使用狀態代碼0觸發回調，並使用相應的錯誤代碼來指示用戶未經過身份驗證。

### 註銷工作流 {#logout}

對於本機客戶端，註銷的處理方式與上述驗證過程類似。 按照此模式，AccessEnabler將建立 `WebView` 控制項，並將使用後端伺服器上註銷終結點的URL載入控制項。 註銷過程完成後，將清除令牌。

請注意，註銷流與驗證流不同，因為用戶不需要與 `WebView` 不管怎樣。 註銷完成後，AccessEnabler將調用 `setAuthenticationStatus()` 回調，狀態代碼為0，表示用戶未經過身份驗證。

## 令牌 {#tokens}

### 定義和使用 {#definitions}

黃金時段身份驗證權利解決方案圍繞在成功完成身份驗證和授權工作流時黃金時段身份驗證生成的特定資料（令牌）的生成。 這些令牌儲存在客戶端的AmazonFireOS設備上。

令牌的壽命有限；到期後，需要通過重新啟動驗證和/或授權工作流來重新發佈令牌。

在權利工作流期間發出的令牌有三種類型：

- **驗證令牌**  — 用戶身份驗證工作流的最終結果將是身份驗證GUID,AccessEnabler可以使用該GUID代表用戶進行授權查詢。 此驗證GUID將具有與用戶的驗證會話本身不同的關聯生存時間(TTL)值。 黃金時間驗證通過將驗證GUID綁定到啟動驗證請求的設備來生成驗證令牌。
- **授權令牌**  — 授予對由唯一 `resourceID`。 其中包括授權方發放的授權補助金及原件 `resourceID`。 此資訊綁定到啟動請求的設備。
- **短命媒體令牌** - AccessEnabler通過返回短時間的媒體令牌，授予對給定資源的托管應用程式的訪問權限。 基於先前為該特定資源獲取的授權令牌生成此令牌。 此外，此令牌未綁定到設備，並且關聯的壽命會顯著縮短(預設值：5分鐘)。

在成功驗證和授權後，黃金時段驗證將發佈驗證、授權和短時間媒體令牌。 這些令牌應快取在用戶設備上，並在其關聯的生命週期內使用。

### 快取准則 {#caching}


#### 驗證令牌

- **AccessEnabler 1.10.1 for FireOS **基於Android 1.9.1的AccessEnabler — 此SDK引入了一種新的令牌儲存方法，使程式設計師 — MVPD儲存桶可以儲存多個身份驗證令牌。 

#### 授權令牌

在任何給定時刻，AccessEnabler只快取每個資源一個授權令牌。 可以快取多個授權令牌，但它們與不同的資源相關聯。 只要頒發了新的授權令牌，並且同一資源的舊授權令牌已存在，新令牌就會覆蓋現有的快取值。

#### 媒體令牌 

根本不應快取短時間的媒體令牌。 每次調用授權API時，應從伺服器中檢索媒體令牌，因為它僅限於一次性使用。

### 持久性 {#persistence}

令牌需要在同一應用程式的連續運行中保持持久性。 這意味著一旦獲得了驗證和授權令牌並且用戶關閉了應用程式，當用戶重新開啟應用程式時，應用程式就可以使用相同的令牌。 此外，這些令牌在多個應用中是持久的。 換句話說，當用戶使用一個應用程式與特定身份提供程式登錄（成功獲取身份驗證和授權令牌）後，同一令牌可以通過不同的應用程式使用，並且當通過同一身份提供程式登錄時不再提示用戶提供憑據。

這種類型的無縫身份驗證/授權工作流使Mogfire身份驗證解決方案成為真正的TV-Everywhere實現。 從純粹的工程角度看，Android AccessEnabler庫通過將令牌資料儲存到位於外部儲存上的資料庫檔案來解決跨應用程式資料共用問題。 此系統級共用資源提供了關鍵要素，這些要素支援實現所需的持久令牌使用情形：

- 支援結構化儲存 — 黃金時段身份驗證令牌儲存不僅是簡單的線性緩衝儲存結構。 它提供了類似於字典的儲存機制，允許基於用戶指定的鍵值進行資料索引。
- 支援使用基礎檔案系統的資料持久性 — 預設情況下，資料庫檔案的內容會保留，資料會保存在設備的外部記憶體上。

將特定令牌放入令牌快取後，AccessEnabler庫將在不同時間檢查其有效性。  有效令牌定義為：

- 令牌的TTL未過期
- 令牌的頒發者包含在允許的身份提供程式清單中

令牌儲存器可支援多個程式設計師 — MVPD組合，依賴於能夠容納多個驗證令牌的多級嵌套映射結構。 此新儲存不會以任何方式影響AccessEnabler公共API，也不需要程式設計師方面的更改。 下面是一個示例，說明了此較新的功能：

1. 開啟App1（由程式設計師1開發）。
1. 通過MVPD1（與Programmer1整合）進行身份驗證。
1. 掛起/關閉當前應用程式，並開啟App2（由Programmer2開發）。
1. 假設程式設計師2未與MVPD2整合；因此，用戶將無法在App2中進行身份驗證。
1. 通過App2中的MVPD2（與Programmer2整合）進行身份驗證。
1. 切換回App1；用戶仍將通過Programmer1進行身份驗證。

### 格式 {#format}

#### 驗證令牌 {#authn_token}

下面的清單顯示驗證令牌的格式：

```JSON
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

```JSON
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


#### 短媒體令牌 {#short_media_token}

以下清單顯示短媒體令牌的格式。  此令牌會暴露給程式設計師的應用程式。  在成功的權利流程結束時，它會傳遞到程式設計師的應用程式：

```JSON
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
 

#### 設備綁定 {#device_binding}

在上面的XML清單中，請注意標題為 `simpleTokenFingerprint`。 此標籤的目的是保存本機設備ID個性化資訊。 AccessEnabler庫能夠獲取這種個性化資訊，並在權利調用期間將其提供給Mogine身份驗證服務。 服務將使用此資訊並將其嵌入到實際令牌中，從而有效地將令牌綁定到特定設備。 最終目標是使令牌不能跨設備傳輸。

在上面的XML清單中，請注意標題為simpleTokenFingrement的標籤。 此標籤的目的是保存本機設備ID個性化資訊。 AccessEnabler庫能夠獲取這種個性化資訊，並在權利調用期間將其提供給Mogine身份驗證服務。 服務將使用此資訊並將其嵌入到實際令牌中，從而有效地將令牌綁定到特定設備。 最終目標是使令牌不能跨設備傳輸。

由於這顯然是與安全相關的功能，因此從安全形度來看，此資訊具有內在的「敏感」性。 因此，需要保護這些資訊不受篡改和竊聽。 通過通過HTTPS協定發送驗證/授權請求來解決竊聽問題。 通過對設備標識資訊進行數字簽名來處理篡改保護。 AccessEnabler庫根據設備提供的資訊計算設備ID，然後將設備ID「在清除中」作為請求參數發送到黃金時段驗證伺服器。  Mighine身份驗證伺服器使用Adobe的私鑰對設備ID進行數字簽名，並將其添加到返回給AccessEnabler的身份驗證令牌中。 因此，設備ID與驗證令牌綁定。  在授權流程中， AccessEnabler再次以清除方式發送設備ID以及驗證令牌。  驗證過程失敗將自動導致驗證/授權工作流失敗。  黃金時段驗證伺服器將私鑰應用到設備ID，並將其與驗證令牌中的值進行比較。  如果它們不匹配，則該權利流將失敗。
