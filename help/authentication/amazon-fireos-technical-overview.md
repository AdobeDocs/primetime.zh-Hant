---
title: Amazon FireOS技術概覽
description: Amazon FireOS技術概覽
exl-id: 939683ee-0dd9-42ab-9fde-8686d2dc0cd0
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---

# Amazon FireOS技術概覽 {#amazon-fireos-technical-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 簡介 {#intro}

Amazon FireOS AccessEnabler由兩個元件表示：一個是應用程式使用的AccessEnabler存根程式庫，另一個是系統層級的Java Android程式庫，可讓行動應用程式使用Adobe Primetime驗證進行TV Everywhere的軟體權利檔案服務。 Amazon FireOS的Android實作包含定義權益API的AccessEnabler介面，以及描述程式庫觸發之回撥的EntitlementDelegate通訊協定。 系統層級AccessEnabler Android資料庫可讓您存取Amazon服務，以在平台層級啟用Single Sing On。

## 瞭解原生使用者端工作流程 {#native_client_workflows}

原生使用者端工作流程通常與瀏覽器型Primetime驗證使用者端的工作流程相同或非常類似。 不過，有一些例外情況，如下所述。


### 初始化後工作流程 {#post-init}

AccessEnabler支援的所有軟體權利檔案工作流程都假設您先前已呼叫 [`setRequestor()`](#setRequestor) 以建立您的身分。 您進行此呼叫是為了只提供請求者ID一次，通常是在應用程式的初始化/設定階段。

與原生使用者端（例如AmazonFireOS）搭配使用，在您初次呼叫 [`setRequestor()`](#setRequestor)，您可以選擇如何繼續：

- 您可以立即開始發出軟體權利檔案呼叫，並視需要允許以靜默方式將其排入佇列。
- 或者，您可以收到成功/失敗的確認 [`setRequestor()`](#setRequestor) 實作setRequestorComplete()回呼。
- 或者，兩者都執行。

至於是否要等待成功的通知，則由您決定。 [`setRequestor()`](#setRequestor) 或依賴AccessEnabler的呼叫佇列機制。 由於所有後續授權和驗證請求都需要請求者ID和相關聯的設定資訊， [`setRequestor()`](#setRequestor) 在初始化完成之前，方法會有效地封鎖所有驗證和授權API呼叫。

### 通用初始驗證工作流程 {#generic}

此工作流程的目的是使用使用者的MVPD登入使用者。  成功登入後，後端伺服器會向使用者發出驗證權杖。 雖然驗證通常作為授權流程的一部分完成，但以下說明如何單獨進行驗證，並且不包括任何授權步驟。

請注意，雖然下列原生使用者端工作流程與典型的瀏覽器驗證工作流程不同，但步驟1-5對原生使用者端和瀏覽器使用者端都相同：

1. 您的頁面或播放器透過呼叫來啟動驗證工作流程 [getAuthentication()](#getAuthN)，會檢查是否有有效的快取驗證Token。 此方法有一個選擇性 `redirectURL` 引數；如果您未提供 `redirectURL`，在成功驗證後，使用者會傳回至初始化驗證的URL。
1. AccessEnabler會判斷目前的驗證狀態。 如果使用者目前已驗證，AccessEnabler會呼叫 `setAuthenticationStatus()` 回呼函式，傳遞表示成功的驗證狀態（下面的步驟7）。
1. 如果使用者未驗證，AccessEnabler會透過判斷使用者的上次驗證嘗試是否在指定的MVPD上成功來繼續驗證流程。 如果已快取MVPD ID且 `canAuthenticate` 標幟為true或選取的MVPD是使用 [`setSelectedProvider()`](#setSelectedProvider)，則不會使用MVPD選取對話方塊提示使用者。 驗證流程會繼續使用MVPD的快取值（即上次成功驗證期間使用的MVPD）。 系統會呼叫後端伺服器，並將使用者重新導向至MVPD登入頁面（下方的步驟6）。
1. 如果未快取MVPD ID且未使用選取MVPD [`setSelectedProvider()`](#setSelectedProvider) 或 `canAuthenticate` 標幟設為false，則 [`displayProviderDialog()`](#displayProviderDialog) 已呼叫callback。 此回呼會引導您的頁面或播放器建立UI，向使用者顯示可從中進行選擇的MVPD清單。 提供了一個MVPD物件陣列，其中包含建立MVPD選擇器所需的資訊。 每個MVPD物件都描述一個MVPD實體，並包含MVPD的ID等資訊（例如XFINITY、AT\&amp;T等） 和可以找到MVPD標誌的URL。
1. 選取特定MVPD後，您的頁面或播放器必須通知AccessEnabler使用者的選擇。 對於非Flash使用者端，一旦使用者選取所需的MVPD，您就會透過呼叫 [`setSelectedProvider()`](#setSelectedProvider) 方法。 Flash使用者端改為傳送共用的 `MVPDEvent` 屬於「」型別`mvpdSelection`&quot;，傳遞選取的提供者。
1. 若為Amazon應用程式， [`navigateToUrl()`](#navigagteToUrl) 將忽略callback。 Access Enabler程式庫有助於存取常見的WebView控制項，以驗證使用者。
1. 透過 `WebView`，使用者就會進入MVPD的登入頁面並輸入其認證。 請注意，在此傳輸期間會發生數個重新導向操作。 
1. 一旦WebView完成驗證，就會關閉並通知AccessEnabler使用者已成功登入，AccessEnabler就會從後端伺服器擷取實際的驗證Token。 AccessEnabler會呼叫 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態碼為1的callback，表示成功。 如果在執行這些步驟期間發生錯誤， [`setAuthenticationStatus()`](#setAuthNStatus) 系統會以狀態碼0觸發回呼，並顯示對應的錯誤代碼，指出使用者未驗證。

### 登出工作流程 {#logout}

對於原生使用者端，登出的處理與上述驗證程式類似。 依照此模式，AccessEnabler將建立 `WebView` 控制和將會在後端伺服器上使用登出端點的URL載入控制。 登出程式完成後，系統會清除Token。

請注意，登出流程與驗證流程不同，因為使用者不需要與 `WebView` 任何方式。 登出完成後，AccessEnabler會呼叫 `setAuthenticationStatus()` 狀態碼為0的callback，表示使用者未驗證。

## Token {#tokens}

### 定義和使用情況 {#definitions}

Primetime驗證許可權解決方案圍繞著產生特定資料片段（代號），Primetime驗證會在成功完成驗證和授權工作流程時產生。 這些Token儲存在使用者端的Amazon FireOS裝置上。

權杖的生命週期有限；到期時，需要透過重新起始驗證和/或授權工作流程重新發行權杖。

在權益工作流程期間會核發三種型別的Token：

- **驗證Token**  — 使用者驗證工作流程的最終結果將是一個驗證GUID，AccessEnabler可以使用它來代表使用者進行授權查詢。 此驗證GUID將具有關聯的存留時間(TTL)值，該值可能與使用者的驗證工作階段本身不同。 Primetime驗證會將驗證GUID繫結至起始驗證要求的裝置，藉此產生驗證權杖。
- **授權權杖**  — 授予對由唯一識別的特定受保護資源的存取權 `resourceID`. 它是由授權方核發的授權授與原始檔案 `resourceID`. 此資訊會繫結至起始請求的裝置。
- **短期媒體權杖** - AccessEnabler會傳回短期的Media Token，授與特定資源之託管應用程式的存取權。 此Token是根據先前為該特定資源取得的授權Token而產生。 此外，此Token不會繫結至裝置，而且關聯的存留期會明顯縮短（預設為： 5分鐘）。

在成功驗證和授權後，Primetime驗證將發佈驗證、授權和短暫的媒體權杖。 這些Token應在使用者裝置上快取，並用於其相關存留期的持續時間。

### 快取准則 {#caching}


#### 驗證Token

- **FireOS適用的AccessEnabler 1.10.1 **以Android 1.9.1適用的AccessEnabler為基礎 — 此SDK推出新的權杖儲存方法，可啟用多個程式設計人員 — MVPD貯體，因此可啟用多個驗證權杖。 

#### 授權Token

在任何指定時刻，AccessEnabler只會快取每個資源一個授權權杖。 可以快取多個授權權杖，但它們與不同資源相關聯。 每當核發新的授權權杖且同一資源已存在舊權杖時，新權杖就會覆寫現有的快取值。

#### 媒體Token 

不應快取短暫的媒體權杖。 每次呼叫授權API時，應該從伺服器擷取媒體權杖，因為它僅限於一次性使用。

### 持續性 {#persistence}

Token必須持續存在於相同應用程式的連續執行中。 這表示取得驗證和授權權杖且使用者關閉應用程式後，當使用者重新開啟應用程式時，應用程式可使用相同的權杖。 此外，這些代號最好在多個應用程式中持續存在。 換言之，當使用者使用一個應用程式來登入特定的身分提供者（成功取得驗證和授權權杖）後，相同的權杖便可以透過不同的應用程式使用，而且當使用者透過相同的身分提供者登入時，不再提示使用者輸入認證。

正是這種無縫的驗證/授權工作流程，使得Primetime驗證解決方案成為真正的TV-Everywhere實施。 從純粹的工程角度來看，Android AccessEnabler程式庫會將代號資料儲存至位於外部儲存裝置的資料庫檔案中，以解決跨應用程式資料共用問題。 此系統層級的共用資源提供可啟用所需永久權杖使用案例實施的關鍵要素：

- 支援結構化儲存 — Primetime驗證Token儲存不僅僅是簡單的線性緩衝記憶體結構。 它提供類似字典的儲存機制，允許根據使用者指定的索引鍵值索引資料。
- 支援使用基礎檔案系統的資料持續性 — 預設會持續儲存資料庫檔案的內容，且資料會儲存在裝置的外部記憶體中。

一旦特定權杖放入權杖快取中，AccessEnabler程式庫就會在不同的時間檢查其有效性。  有效的Token定義為：

- 權杖的TTL尚未過期
- 權杖的簽發者包含在允許的身分提供者清單中

權杖儲存可支援多個Programmer-MVPD組合，仰賴可容納多個驗證權杖的多層級巢狀對應結構。 此新儲存裝置不會以任何方式影響AccessEnabler公用API，而且程式設計人員不需要變更。 以下範例說明這項較新功能：

1. 開啟App1 （由程式設計人員1開發）。
1. 使用MVPD1 （與程式設計人員1整合）進行驗證。
1. 暫停/關閉目前的應用程式，然後開啟App2 （由程式設計人員2開發）。
1. 假設程式設計師2未與MVPD2整合；因此，使用者將不會在App2中驗證。
1. 在App2中使用MVPD2 （與程式設計人員2整合）進行驗證。
1. 切換回App1；使用者仍將透過程式設計人員1進行驗證。

### 格式 {#format}

#### 驗證Token {#authn_token}

以下清單顯示驗證Token的格式：

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
 

#### 授權Token {#authz_token}

以下清單顯示授權權杖的格式：

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


#### 短媒體Token {#short_media_token}

以下清單顯示短媒體權杖的格式。  此Token會公開給程式設計師的應用程式。  它會在成功的軟體權利檔案程式結束時傳遞給程式設計師的應用程式：

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
 

#### 裝置繫結 {#device_binding}

在上面的XML清單中，記下標題為 `simpleTokenFingerprint`. 此標籤的用途是儲存原生裝置ID個人化資訊。 AccessEnabler程式庫可取得這類個人化資訊，並在軟體權利檔案呼叫期間提供給Primetime驗證服務。 此服務會使用此資訊，並將其內嵌於實際Token中，以有效地將Token繫結至特定裝置。 此動作的最終目標是讓代號無法跨裝置傳輸。

在上述XML清單中，請注意名為simpleTokenFingerprint的標籤。 此標籤的用途是儲存原生裝置ID個人化資訊。 AccessEnabler程式庫可取得這類個人化資訊，並在軟體權利檔案呼叫期間提供給Primetime驗證服務。 此服務會使用此資訊，並將其內嵌於實際Token中，以有效地將Token繫結至特定裝置。 此動作的最終目標是讓代號無法跨裝置傳輸。

由於這顯然是安全性相關功能，因此從安全性角度來看，此資訊本身就具有「敏感性」。 因此，需要保護此資訊不被竄改和竊聽。 透過透過HTTPS通訊協定傳送驗證/授權請求，即可解決竊聽問題。 篡改保護是透過數位簽署裝置識別資訊來處理。 AccessEnabler程式庫會從裝置提供的資訊計算裝置ID，然後將裝置ID「完全清除」傳送至Primetime驗證伺服器，作為要求引數。  Primetime驗證伺服器會使用Adobe的私密金鑰數位簽署裝置ID，並將其新增至傳回AccessEnabler的驗證權杖。 因此，裝置ID會與驗證Token繫結。  在授權流程期間，AccessEnabler會再次在清除中傳送裝置ID以及驗證Token。  驗證程式的失敗將自動導致驗證/授權工作流程失敗。  Primetime驗證伺服器會將私密金鑰套用至裝置ID，並將其與驗證權杖中的值比較。  如果兩者不相符，該權益流程就會失敗。
