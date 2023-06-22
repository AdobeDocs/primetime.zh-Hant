---
title: Android SDK概觀
description: Android SDK概觀
exl-id: a1d98325-32a1-4881-8635-9a3c38169422
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 0%

---

# Android SDK概觀 {#android-sdk-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>


## 簡介 {#intro}

Android AccessEnabler是Java Android資料庫，可讓行動應用程式使用Adobe Primetime驗證進行TV Everywhere的軟體權利服務。 Android實施包含定義軟體權利檔案API的AccessEnabler介面，以及描述程式庫觸發之回撥的EntitlementDelegate通訊協定。 介面與通訊協定參照在一個通用名稱下：AccessEnabler Android程式庫。

## Android需求 {#reqs}

如需與Android平台和Primetime驗證相關的目前技術需求，請參閱 [平台/裝置/工具需求](#android)，或參閱Android SDK下載專案包含的發行說明。

## 瞭解原生使用者端工作流程 {#native_client_workflows}

原生使用者端工作流程通常與瀏覽器型Primetime驗證使用者端的工作流程相同或非常類似。 不過，有一些例外情況，如下所述。

- [初始化後工作流程](#post-init)
- [通用初始驗證工作流程](#generic)
- [登出工作流程](#logout)



### 初始化後工作流程 {#post-init}

AccessEnabler支援的所有軟體權利檔案工作流程都假設您先前已呼叫 [`setRequestor()`](#setRequestor) 以建立您的身分。 您進行此呼叫是為了只提供請求者ID一次，通常是在應用程式的初始化/設定階段。


使用原生使用者端（例如Android），在您初次呼叫後 [`setRequestor()`](#setRequestor)，您可以選擇如何繼續：

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
1. 針對Android應用程式，如果com.android.chrome可供使用，則驗證URL將會載入Chrome自訂標籤中。
1. 透過Chrome自訂標籤，使用者到達MVPD的登入頁面並輸入其認證。 請注意，在此傳輸期間會發生數個重新導向操作。
1. 當Chrome自訂標籤偵測到URL符合配置(adobepass://)和資源「redirect\_uri」(即adobepass://com.adobepass )的深層連結時，AccessEnabler會從後端伺服器擷取實際的驗證Token。 請注意，最終重新導向URL實際上無效，Chrome自訂標籤並非打算實際載入這些URL。 它們只能由SDK解譯為驗證流程已完成的訊號。
1. AccessEnabler會通知您的應用程式驗證流程已完成。 AccessEnabler會呼叫 [`setAuthenticationStatus()`](#setAuthNStatus) 狀態碼為1的callback，表示成功。 如果在執行這些步驟期間發生錯誤， [`setAuthenticationStatus()`](#setAuthNStatus) 系統會以狀態碼0觸發回呼，並顯示對應的錯誤代碼，指出驗證失敗。

### 登出工作流程 {#logout}

對於原生使用者端，登出的處理與上述驗證程式類似。 依照此模式，AccessEnabler會開啟Chrome自訂標籤，並在後端伺服器上載入登出端點的URL。



**注意：** 從某個程式設計人員/MVPD工作階段登出將會清除該特定MVPD的基礎儲存，包括透過該裝置上的SSO取得的所有其他程式設計人員驗證權杖。 不會刪除為其他MVPD取得或未透過SSO取得的Token。 


## Token {#tokens}

- [定義和使用情況](#definitions)
- [快取准則](#caching)
- [持續性](#persistence)
- [格式](#format)
- [裝置繫結](#device_binding)



### 定義和使用情況 {#definitions}

Primetime驗證許可權解決方案圍繞著產生特定資料片段（代號），Primetime驗證會在成功完成驗證和授權工作流程時產生。 這些Token會儲存在使用者端的Android裝置上。

權杖的生命週期有限；到期時，需要透過重新起始驗證和/或授權工作流程重新發行權杖。

在權益工作流程期間會核發三種型別的Token：

- **驗證Token**  — 使用者驗證工作流程的最終結果將是一個驗證GUID，AccessEnabler可以使用它來代表使用者進行授權查詢。 此驗證GUID將具有關聯的存留時間(TTL)值，該值可能與使用者的驗證工作階段本身不同。 Primetime驗證會將驗證GUID繫結至起始驗證要求的裝置，藉此產生驗證權杖。
- **授權權杖**  — 授予對由唯一識別的特定受保護資源的存取權 `resourceID`. 它是由授權方核發的授權授與原始檔案 `resourceID`. 此資訊會繫結至起始請求的裝置。
- **短期媒體權杖** - AccessEnabler會傳回短期的Media Token，授與特定資源之託管應用程式的存取權。 此Token是根據先前為該特定資源取得的授權Token而產生。 此外，此Token不會繫結至裝置，而且關聯的存留期會明顯縮短（預設為： 5分鐘）。

在成功驗證和授權後，Primetime驗證將發佈驗證、授權和短暫的媒體權杖。 這些權杖應在使用者裝置上快取，並用於其相關存留期的持續時間。



### 快取准則 {#caching}

- 驗證Token
- 授權Token
- 媒體Token


#### 驗證Token

- **AccessEnabler 1.6及舊版** - ****在裝置上快取驗證Token的方式取決於&quot;**每個請求者的驗證」** 與目前MVPD關聯的旗標：


1. 如果「每個請求者的驗證」功能為 *已停用*，則單一驗證Token會儲存在全域剪貼簿的本機。 此代號將在與目前MVPD整合的所有應用程式之間共用。
1. 如果「每個請求者的驗證」功能為 *已啟用*，則Token會明確與執行驗證流程的Programmer相關聯（Token不會儲存在全域剪貼簿中，而是儲存在只能供該Programmer的應用程式使用的私人檔案中）。 更具體來說，將會停用不同應用程式之間的單一登入(SSO)；使用者在切換至新應用程式時，需要明確執行驗證流程（前提是第二個應用程式的程式設計師已整合至目前的MVPD，而且本機快取中沒有該程式設計師的驗證權杖）。

   **注意：** AE 1.6 Google GSON技術說明： [如何解析Gson相依性](https://tve.zendesk.com/entries/22902516-Android-AccessEnabler-1-6-How-to-resolve-Gson-dependencies)

- **AccessEnabler 1.7**  — 此SDK推出新的權杖儲存方法，可啟用多個程式設計師 — MVPD貯體，因此可啟用多個驗證Token。 從AE 1.7開始，「每位請求者的驗證」案例和一般驗證流程都會使用相同的儲存配置。 兩者之間唯一的差異在於執行驗證的方式：「每位請求者的驗證」包含一項新的改善（被動驗證），使AccessEnabler能夠根據儲存體中的驗證權杖執行後端通道驗證（針對不同的程式設計人員）。 使用者只需驗證一次，此工作階段將用於取得後續應用程式中的驗證Token。 此反向管道流程會於 [`setRequestor()`](#setRequestor) 呼叫，且對程式設計人員來說大多是透明的。 然而，這裡有一個重要的要求：程式設計師必須呼叫 [`setRequestor()`](#setRequestor) 從主要UI執行緒和活動內。 


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



從AccessEnabler 1.7開始，權杖儲存可支援多個Programmer-MVPD組合，依賴可容納多個驗證權杖的多層巢狀對應結構。 此新儲存裝置不會以任何方式影響AccessEnabler公用API，而且程式設計人員不需要變更。 以下範例說明這項較新功能：

1. 開啟App1 （由程式設計人員1開發）。
1. 使用MVPD1 （與程式設計人員1整合）進行驗證。
1. 暫停/關閉目前的應用程式，然後開啟App2 （由程式設計人員2開發）。
1. 假設程式設計師2未與MVPD2整合；因此，使用者將不會在App2中驗證。
1. 在App2中使用MVPD2 （與程式設計人員2整合）進行驗證。
1. 切換回App1；使用者仍將透過程式設計人員1進行驗證。

在舊版AccessEnabler中，步驟6會將使用者轉譯為未驗證，因為權杖儲存先前僅支援一個驗證權杖。


**注意：** 從某個程式設計人員/MVPD工作階段登出將會清除基礎儲存，包括具有SSO的裝置上的所有其他程式設計人員驗證Token。 不會刪除為其他MVPD取得或未透過SSO取得的Token。 取消驗證流程(叫用 [`setSelectedProvider(null)`](#setSelectedProvider))不會清除基礎儲存體，但只會影響目前的程式設計人員/MVPD驗證嘗試（清除目前程式設計人員的MVPD）。


AccessEnabler 1.7中包含的另一個儲存相關功能，可讓您從較舊的儲存區域匯入驗證權杖。 此「Token Importer」有助於實現連續AccessEnabler版本之間的相容性，即使在儲存版本升級時也能維持SSO狀態。 

匯入工具會在以下期間執行： [`setRequestor()`](#setRequestor) 流程，並在以下兩種情況下執行（假設目前存放區中沒有目前程式設計師的有效驗證Token）：

- 首次安裝由特定程式設計師開發的1.7版應用程式
- 升級路徑至使用新儲存裝置的未來AccessEnabler

匯入作業對程式設計人員而言是透明的，不需要在使用者端應用程式中進行任何程式碼變更。



### 格式 {#format}

- [驗證Token](#authn_token)
- [授權Token](#authz_token)
- [短媒體Token](#short_media_token)
- [裝置繫結](#device_binding)

#### 驗證Token {#authn_token}

以下清單顯示驗證Token的格式：

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

以下清單顯示授權權杖的格式：

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


#### 短媒體Token {#short_media_token}

以下清單顯示短媒體權杖的格式。  此Token會公開給程式設計師的應用程式。  它會在成功的軟體權利檔案程式結束時傳遞給程式設計師的應用程式：

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
 

#### 裝置繫結 {#device_binding}

在上面的XML清單中，記下標題為 `simpleTokenFingerprint`. 此標籤的用途是儲存原生裝置ID個人化資訊。 AccessEnabler程式庫可取得這類個人化資訊，並在軟體權利檔案呼叫期間提供給Primetime驗證服務。 此服務會使用此資訊，並將其內嵌於實際Token中，以有效地將Token繫結至特定裝置。 此動作的最終目標是讓代號無法跨裝置傳輸。



在上述XML清單中，請注意名為simpleTokenFingerprint的標籤。 此標籤的用途是儲存原生裝置ID個人化資訊。 AccessEnabler程式庫可取得這類個人化資訊，並在軟體權利檔案呼叫期間提供給Primetime驗證服務。 此服務會使用此資訊，並將其內嵌於實際Token中，以有效地將Token繫結至特定裝置。 此動作的最終目標是讓代號無法跨裝置傳輸。



由於這明顯是一項安全性相關功能，因此從安全性角度來看，此資訊原本就具有「敏感性」。 因此，需要保護此資訊不被竄改和竊聽。 透過透過HTTPS通訊協定傳送驗證/授權請求，即可解決竊聽問題。 篡改保護是透過數位簽署裝置識別資訊來處理。 AccessEnabler程式庫會從裝置提供的資訊計算裝置ID，然後將裝置ID「完全清除」傳送至Primetime驗證伺服器，作為要求引數。  Primetime驗證伺服器會使用Adobe的私密金鑰數位簽署裝置ID，並將其新增至傳回AccessEnabler的驗證權杖。 因此，裝置ID會與驗證Token繫結。  在授權流程期間，AccessEnabler會再次在清除中傳送裝置ID以及驗證Token。  驗證程式的失敗將自動導致驗證/授權工作流程失敗。  Primetime驗證伺服器會將私密金鑰套用至裝置ID，並將其與驗證權杖中的值比較。  如果兩者不相符，該權益流程就會失敗。


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
