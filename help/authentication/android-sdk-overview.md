---
title: Android SDK概述
description: Android SDK概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 0%

---



# Android SDK概述 {#android-sdk-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>


## 簡介 {#intro}

Android AccessEnabler是Java Android資料庫，可讓行動應用程式對TV Everywhere的權益服務使用Adobe Primetime驗證。 Android實作包含定義權限API的AccessEnabler介面，以及描述程式庫觸發回呼的EntitlementDelegate通訊協定。 該介面與協定以一個通用名稱引用：AccessEnabler Android庫。

## Android需求 {#reqs}

如需與Android平台和Primetime驗證相關的目前技術需求，請參閱 [平台/裝置/工具需求](#android)，或參閱Android SDK下載隨附的發行說明。

## 了解原生用戶端工作流程 {#native_client_workflows}

原生用戶端工作流程通常與瀏覽器型Primetime驗證用戶端的工作流程相同或非常類似。 但是，有一些例外，如下所述。

- [初始化後工作流](#post-init)
- [一般初始驗證工作流程](#generic)
- [登出工作流程](#logout)



### 初始化後工作流 {#post-init}

AccessEnabler支援的所有權利工作流假定您以前已調用 [`setRequestor()`](#setRequestor) 來確認你的身份。 您發出此呼叫時，通常只會在應用程式的初始化/設定階段期間提供要求者ID一次。


在您初次呼叫 [`setRequestor()`](#setRequestor)，您可以選擇如何繼續：

- 您可以立即開始進行權限呼叫，並視需要允許他們以靜默方式佇列。

- 或者，您可以收到 [`setRequestor()`](#setRequestor) 透過實作setRequestorComplete()回呼。

- 或者，兩者兼而有之。

是否等待成功通知由您決定 [`setRequestor()`](#setRequestor) 或依賴AccessEnabler的呼叫隊列機制。 由於所有後續的授權和驗證請求都需要請求者ID和相關的配置資訊，因此， [`setRequestor()`](#setRequestor) 方法會有效封鎖所有驗證和授權API呼叫，直到初始化完成為止。

 

### 一般初始驗證工作流程 {#generic}

此工作流程的用途是使用其MVPD登入使用者。  成功登入後，後端伺服器會向使用者發出驗證Token。 雖然驗證通常是在授權過程中完成的，但以下說明如何隔離進行驗證，並且不包括任何授權步驟。

請注意，雖然下列原生用戶端工作流程與一般的瀏覽器式驗證工作流程不同，但原生用戶端和瀏覽器式用戶端的步驟1至5都相同：

1. 您的頁面或播放器會以呼叫 [getAuthentication()](#getAuthN)，會檢查是否有有效的快取驗證Token。 此方法有選用 `redirectURL` 參數；如果您未為 `redirectURL`，在成功驗證後，會將使用者傳回驗證初始化的URL。
1. AccessEnabler確定當前的身份驗證狀態。 如果用戶當前已通過驗證，則AccessEnabler將調用 `setAuthenticationStatus()` 回呼函式，傳遞表示成功的驗證狀態（下方步驟7）。
1. 如果未驗證用戶，AccessEnabler將通過確定用戶的上次驗證嘗試是否在給定MVPD下成功來繼續驗證流。 如果已快取MVPD ID，且 `canAuthenticate` 標幟為true，或已使用 [`setSelectedProvider()`](#setSelectedProvider)，系統不會以MVPD選取對話方塊提示使用者。 驗證流程會繼續使用MVPD的快取值（亦即上次成功驗證期間使用的相同MVPD）。 系統會對後端伺服器發出網路呼叫，並將使用者重新導向至MVPD登入頁面（下方的步驟6）。
1. 如果未快取任何MVPD ID，且未使用 [`setSelectedProvider()`](#setSelectedProvider) 或 `canAuthenticate` 標幟設為false, [`displayProviderDialog()`](#displayProviderDialog) 呼叫回呼。 此回撥會引導您的頁面或播放器建立UI，此UI會向使用者顯示要選擇的MVPD清單。 提供MVPD物件的陣列，其中包含您建立MVPD選取器的必要資訊。 每個MVPD物件都描述MVPD實體，並包含MVPD的ID（例如XFINITY、AT\&amp;T等）等資訊 和可找到MVPD標誌的URL。
1. 選取特定MVPD後，您的頁面或播放器必須通知AccessEnabler使用者的選擇。 對於非Flash客戶端，一旦用戶選擇了所需的MVPD，您就通過對 [`setSelectedProvider()`](#setSelectedProvider) 方法。 Flash客戶端改為發送共用 `MVPDEvent` 類型&quot;`mvpdSelection`&quot;，傳遞所選提供程式。
1. 若為Android應用程式，若com.android.chrome可用，驗證URL將會在Chrome自訂分頁中載入。
1. 透過Chrome自訂分頁，使用者進入MVPD的登入頁面並輸入其憑證。 請注意，此傳輸期間會發生數個重新導向操作。
1. 當Chrome自訂分頁偵測到URL符合配置(adobepass://)以及資源「redirect\_uri」(即adobepass://com.adobepass)的深層連結時，AccessEnabler會從後端伺服器擷取實際驗證Token。 請注意，最終的重新導向URL實際上無效，且這些URL並非供Chrome自訂分頁實際載入。 SDK只能將其解讀為驗證流程已完成的訊號。
1. AccessEnabler通知您的應用程式驗證流程已完成。 AccessEnabler將調用 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態代碼為1的回呼表示成功。 如果執行這些步驟期間發生錯誤，則 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態碼為0時觸發回呼，並附上相應的錯誤碼，表示驗證失敗。

### 登出工作流程 {#logout}

對於本機用戶端，登出的處理方式與上述驗證程式類似。 依照此模式，AccessEnabler會開啟「Chrome自訂」標籤，並載入後端伺服器上登出端點的URL。



**注意：** 從一個程式設計師/MVPD會話註銷將清除該特定MVPD的基礎儲存，包括通過該設備上的SSO獲得的所有其他程式設計師身份驗證令牌。 不會刪除為其他MVPD或未透過SSO取得的代號。 


## 代號 {#tokens}

- [定義與使用](#definitions)
- [快取准則](#caching)
- [持久性](#persistence)
- [格式](#format)
- [設備綁定](#device_binding)



### 定義與使用 {#definitions}

Primetime驗證權限解決方案的核心是產生特定資料片段（代號），這些資料片段（代號）是Primetime驗證在成功完成驗證和授權工作流程後所產生。 這些代號會儲存在用戶端的Android裝置上。

代號的有效期有限；到期時，需透過重新啟動驗證和/或授權工作流程來重新核發權杖。

在權限工作流程期間發出的代號有三種：

- **驗證Token**  — 用戶驗證工作流的最終結果將是驗證GUID,AccessEnabler可以使用它代表用戶進行授權查詢。 此驗證GUID會有與使用者驗證工作階段本身不同的相關存留時間(TTL)值。 Primetime驗證會將驗證GUID系結至啟動驗證請求的裝置，借此產生驗證Token。
- **授權Token**  — 授予對由唯一 `resourceID`. 它由授權方發出的授權授權，連同原始授權 `resourceID`. 此資訊會系結至起始請求的裝置。
- **短期媒體代號** - AccessEnabler通過返回短期媒體令牌來授予對給定資源的托管應用程式的訪問權限。 該令牌基於先前為該特定資源獲取的授權令牌而生成。 此外，此代號未系結至裝置，且相關的生命週期會明顯縮短(預設值：5分鐘)。

成功驗證和授權後，Primetime驗證會發出驗證、授權和短期媒體權杖。 這些代號應在使用者裝置上快取，並在其相關聯的有效期內使用。



### 快取准則 {#caching}

- 驗證Token
- 授權Token
- 媒體代號


#### 驗證Token

- **AccessEnabler 1.6及更舊版本** - ****在裝置上快取驗證Token的方式取決於&#x200B;**每個請求者的身份驗證」** 與目前MVPD相關聯的標幟：


1. 如果「每個請求者的驗證」功能為 *停用*，則單一驗證Token會儲存在全域貼上板的本機。 此代號將在與目前MVPD整合的所有應用程式之間共用。
1. 如果「每個請求者的驗證」功能為 *已啟用*，則令牌將與執行驗證流的程式設計師明確關聯（令牌不會儲存在全局貼上板中，而是儲存在只能訪問該程式設計師應用程式的專用檔案中）。 更具體地說，將禁用不同應用程式之間的單一登錄(SSO);當切換到新應用時，用戶需要顯式地執行驗證流（前提是第二應用的程式設計師與當前MVPD整合，並且本地快取中不存在該程式設計師的驗證令牌）。

   **注意：** AE 1.6Google GSON技術說明： [如何解析Gson依賴項](https://tve.zendesk.com/entries/22902516-Android-AccessEnabler-1-6-How-to-resolve-Gson-dependencies)

- **AccessEnabler 1.7**  — 本SDK推出新的權杖儲存方法，可啟用多個程式設計人員 — MVPD貯體，因此可啟用多個驗證權杖。 從AE 1.7開始，「每個請求者身份驗證」方案和正常身份驗證流程都使用相同的儲存佈局。 兩者的唯一差異在於驗證的執行方式：「每個請求者的身份驗證」包含一項新的改進（被動身份驗證），該改進使AccessEnabler能夠基於儲存器中的身份驗證令牌（對於不同的程式設計師）執行後通道身份驗證。 使用者只需驗證一次，此工作階段即可用於在後續應用程式中取得驗證Token。 此後通道流會於 [`setRequestor()`](#setRequestor) 呼叫，對程式設計人員大都透明。 然而，這裡有一個重要要求：程式設計師必須 [`setRequestor()`](#setRequestor) 從主要UI執行緒和活動內。 


#### 授權Token

在任何給定時刻，AccessEnabler都只快取每個資源的一個授權令牌。 可快取多個授權Token，但它們與不同資源相關聯。 每當發出新授權權杖，且相同資源已存在舊權杖時，新權杖會覆寫現有的快取值。



#### 媒體代號 

完全不應快取短期媒體代號。 每次呼叫授權API時，應從伺服器擷取媒體代號，因為此API限制為一次性使用。



### 持久性 {#persistence}

Token必須在相同應用程式的連續執行中持續存在。 這表示一旦取得驗證和授權權杖，且使用者關閉應用程式，當使用者重新開啟應用程式時，應用程式即可使用相同的權杖。 此外，希望這些令牌能跨多個應用程式持續存在。 換言之，當使用者使用一個應用程式以特定身分提供者登入（成功取得驗證和授權權杖）後，相同的權杖可透過不同應用程式使用，且當透過相同身分提供者登入時，不再提示使用者提供憑證。



這類無縫驗證/授權工作流程讓Primetime驗證解決方案成為真正的TV-Everywhere實作。 從純粹的工程角度來看，Android AccessEnabler庫通過將令牌資料儲存到位於外部儲存上的資料庫檔案中來解決跨應用程式資料共用的問題。 此系統層級的共用資源提供可實施所需永久性代號使用案例的關鍵要素：

- 支援結構化儲存 — Primetime驗證權杖儲存不只是簡單的線性緩衝式記憶體結構。 它提供類似字典的儲存機制，允許根據用戶指定的鍵值進行資料索引。
- 使用基礎檔案系統支援資料持續性 — 預設情況下，資料庫檔案的內容會保存，且資料會儲存在裝置的外部記憶體中。



將特定令牌放入令牌快取後，AccessEnabler庫將在不同時間檢查其有效性。  有效的Token定義為：

- 代號的TTL尚未過期
- 令牌的頒發者包含在允許的身分提供者清單中



從AccessEnabler 1.7開始，令牌儲存器可以支援多個程式設計師 — MVPD組合，它依賴於可以容納多個身份驗證令牌的多級嵌套映射結構。 此新儲存不會以任何方式影響AccessEnabler公共API，並且不需要在程式設計師端進行更改。 以下範例說明此較新的功能：

1. 開啟App1（由Programmer1開發）。
1. 使用MVPD1（與Programmer1整合）進行驗證。
1. 暫停/關閉當前應用程式，並開啟App2（由程式設計師2開發）。
1. 假設Programmer2未與MVPD2整合；因此，使用者「不會」在App2中進行驗證。
1. 在App2中使用MVPD2（與Programmer2整合）進行驗證。
1. 切換回App1；用戶仍將通過Programmer1進行身份驗證。

在舊版AccessEnabler中，步驟6會將用戶顯示為未驗證，因為令牌儲存以前僅支援一個驗證令牌。


**注意：** 從一個程式設計師/MVPD會話註銷將清除基礎儲存，包括使用SSO的設備上的所有其他程式設計師身份驗證令牌。 不會刪除為其他MVPD或未透過SSO取得的代號。 取消驗證流程(調用 [`setSelectedProvider(null)`](#setSelectedProvider))不會清除基礎儲存，但只會影響當前程式設計師/ MVPD驗證嘗試（通過擦除當前程式設計師的MVPD）。


AccessEnabler 1.7中包含的另一個與儲存相關的功能使從舊儲存區域導入身份驗證令牌成為可能。 此「令牌導入程式」有助於實現連續AccessEnabler版本之間的相容性，即使在升級儲存版本時，也能保持SSO狀態。 

匯入工具會在 [`setRequestor()`](#setRequestor) 流，並在以下兩種情況下運行（假設當前儲存中不存在當前程式設計師的有效身份驗證令牌）:

- 由特定程式設計師開發的1.7應用程式的首次安裝
- 將路徑升級到使用新儲存的未來AccessEnabler

導入操作對程式設計師是透明的，不需要在客戶端應用程式中進行任何代碼更改。



### 格式 {#format}

- [驗證Token](#authn_token)
- [授權Token](#authz_token)
- [短媒體代號](#short_media_token)
- [設備綁定](#device_binding)

#### 驗證Token {#authn_token}

下列清單顯示驗證Token的格式：

```XML
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

```XML
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


#### 短媒體代號 {#short_media_token}

以下清單顯示簡短媒體代號的格式。  此令牌會向程式設計師的應用程式公開。  在成功的授權過程結束時，它會傳遞到程式設計師的應用程式：

```XML
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

在上方的XML清單中，記下標題為 `simpleTokenFingerprint`. 此標籤的用途是保留原生裝置ID個人化資訊。 AccessEnabler庫能夠獲取此類個性化資訊，並使其在權限調用期間可供Primetime身份驗證服務使用。 服務會使用此資訊並將其內嵌於實際的Token中，借此有效將Token系結至特定裝置。 其最終目標是讓代號不可跨裝置轉讓。



在上方的XML清單中，記下標題為simpleTokenFingerprint的標籤。 此標籤的用途是保留原生裝置ID個人化資訊。 AccessEnabler庫能夠獲取此類個性化資訊，並使其在權限調用期間可供Primetime身份驗證服務使用。 服務會使用此資訊並將其內嵌於實際的Token中，借此有效將Token系結至特定裝置。 其最終目標是讓代號不可跨裝置轉讓。



由於這顯然是與安全相關的功能，因此從安全性角度來看，此資訊本身就是「敏感」的。 因此，需要保護這些資訊不受篡改和竊聽。 通過HTTPS協定發送身份驗證/授權請求來解決竊聽問題。 通過數字簽名設備標識資訊來處理篡改保護。 AccessEnabler庫根據設備提供的資訊計算設備ID，然後將設備ID「在清除中」作為請求參數發送到Primetime驗證伺服器。  Primetime驗證伺服器使用Adobe的私密金鑰對裝置ID進行數位簽署，並將其新增至傳回至AccessEnabler的驗證Token。 因此，裝置ID與驗證Token系結。  在授權流程中，AccessEnabler會再次以清除方式發送設備ID以及驗證令牌。  驗證程式失敗會自動導致驗證/授權工作流程失敗。  Primetime驗證伺服器會將私密金鑰套用至裝置ID，並與驗證Token中的值比較。  如果兩者不相符，則授權流程會失敗。


<!--
## Related Information {#related}

- [Android Integration Cookbook](#)
- [Android API](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime authentication native SDK (Tech Note)](#)
- [AE 1.6: How to resolve Gson dependencies (Tech Note)](#)
-->
