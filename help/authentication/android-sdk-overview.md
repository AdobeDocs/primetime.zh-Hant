---
title: Android SDK總覽
description: Android SDK總覽
exl-id: a1d98325-32a1-4881-8635-9a3c38169422
source-git-commit: 4b858a06080ec221c60548e2a2a0f3b6010ede15
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 0%

---

# Android SDK總覽 {#android-sdk-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

</br>


## 簡介 {#intro}

Android AccessEnabler是Java Android資料庫，可讓行動應用程式使用Adobe Primetime驗證來進行TV Everywhere的權益服務。 Android實施包含定義軟體權利檔案API的AccessEnabler介面，以及描述程式庫觸發之回呼的EntitlementDelegate通訊協定。 介面與通訊協定參照於一個通用名稱下：AccessEnabler Android程式庫。

## Android需求 {#reqs}

如需與Android平台和Primetime驗證相關的目前技術需求，請參閱 [平台/裝置/工具需求](#android)，或參閱Android SDK下載專案隨附的發行說明。

## 瞭解原生使用者端工作流程 {#native_client_workflows}

原生使用者端工作流程通常與瀏覽器型Primetime驗證使用者端的工作流程相同或非常類似。 不過，有一些例外，如下所述。

- [初始化後工作流程](#post-init)
- [通用初始驗證工作流程](#generic)
- [登出工作流程](#logout)



### 初始化後工作流程 {#post-init}

AccessEnabler支援的所有權益工作流程都假設您先前已呼叫 [`setRequestor()`](#setRequestor) 以建立您的身分。 您進行此呼叫時，通常是在應用程式的初始化/設定階段，只提供一次請求者ID。


與原生使用者端（例如Android）搭配使用，在您初次呼叫 [`setRequestor()`](#setRequestor)，您可以選擇如何繼續：

- 您可以立即開始發出權益呼叫，並視需要允許以靜默方式將其排入佇列。

- 或者，您可以收到成功/失敗的確認 [`setRequestor()`](#setRequestor) 實作setRequestorComplete()回呼。

- 或者，兩者都執行。

至於是否要等待成功的通知，則由您決定。 [`setRequestor()`](#setRequestor) 或依賴AccessEnabler的呼叫佇列機制。 由於所有後續授權和驗證請求都需要請求者ID和相關聯的設定資訊， [`setRequestor()`](#setRequestor) 方法會有效地封鎖所有驗證和授權API呼叫，直到初始化完成為止。



### 通用初始驗證工作流程 {#generic}

此工作流程的用途是使用其MVPD登入使用者。  成功登入後，後端伺服器會向使用者發出驗證權杖。 雖然驗證通常是作為授權流程的一部分完成的，但以下說明如何單獨進行驗證，並且不包括任何授權步驟。

請注意，雖然下列原生使用者端工作流程與一般瀏覽器驗證工作流程不同，但原生使用者端和瀏覽器使用者端的步驟1-5均相同：

1. 您的頁面或播放器會透過呼叫來啟動驗證工作流程 [getAuthentication()](#getAuthN)，會檢查是否有有效的快取驗證Token。 此方法有一個選擇性 `redirectURL` 引數；如果未提供 `redirectURL`，在成功驗證後，使用者會回到初始化驗證的URL。
1. AccessEnabler決定目前的驗證狀態。 如果使用者目前已驗證，AccessEnabler會呼叫 `setAuthenticationStatus()` 回呼函式，傳遞表示成功的驗證狀態（下面的步驟7）。
1. 如果使用者未驗證，則AccessEnabler會透過判斷使用者的上次驗證嘗試是否在指定的MVPD上成功來繼續驗證流程。 如果已快取MVPD ID且 `canAuthenticate` 標幟為true或使用 [`setSelectedProvider()`](#setSelectedProvider)，使用者不會因為MVPD選取對話方塊而收到提示。 驗證流程會繼續使用MVPD的快取值（也就是上次成功驗證期間使用的MVPD）。 系統會呼叫後端伺服器的網路，並將使用者重新導向至MVPD登入頁面（下方的步驟6）。
1. 如果未快取任何MVPD ID，且未使用選取任何MVPD [`setSelectedProvider()`](#setSelectedProvider) 或 `canAuthenticate` 標幟設為false，則 [`displayProviderDialog()`](#displayProviderDialog) 系統會呼叫callback。 此回呼會引導您的頁面或播放器建立UI，向使用者顯示可從中進行選擇的MVPD清單。 提供了一系列MVPD物件，其中包含您建置MVPD選取器所需的資訊。 每個MVPD物件描述MVPD實體，並包含MVPD的ID等資訊（例如XFINITY、AT\&amp;T等） 和可以找到MVPD標誌的URL。
1. 選取特定MVPD後，您的頁面或播放器必須通知AccessEnabler使用者的選擇。 對於非Flash使用者端，一旦使用者選取想要的MVPD，您會透過呼叫 [`setSelectedProvider()`](#setSelectedProvider) 方法。 Flash使用者端改為傳送共用的 `MVPDEvent` 屬於「」型別`mvpdSelection`「」，傳遞選取的提供者。
1. 針對Android應用程式，如果com.android.chrome可供使用，則驗證URL將會載入Chrome自訂分頁中。
1. 透過Chrome自訂標籤，使用者到達MVPD的登入頁面並輸入其認證。 請注意，在此傳輸期間會發生數個重新導向作業。
1. 當Chrome自訂標籤偵測到URL符合配置(adobepass://)和資源「redirect\_uri」的深層連結(即adobepass://com.adobepass )時，AccessEnabler會從後端伺服器擷取實際的驗證Token。 請注意，最終重新導向URL實際上無效，且不可供Chrome自訂標籤實際載入。 它們必須由SDK解譯為驗證流程已完成的訊號。
1. AccessEnabler會通知應用程式驗證流程已完成。 AccessEnabler呼叫 [`setAuthenticationStatus()`](#setAuthNStatus) 具有狀態代碼1的回呼，表示成功。 如果在執行這些步驟期間發生錯誤， [`setAuthenticationStatus()`](#setAuthNStatus) 系統會以狀態碼0觸發回呼，並顯示對應的錯誤代碼，表示驗證失敗。

### 登出工作流程 {#logout}

對於原生使用者端，登出的處理與上述驗證程式類似。 依照此模式，AccessEnabler會開啟Chrome自訂標籤，並在後端伺服器上載入登出端點的URL。



**注意：** 從某個程式設計人員/MVPD工作階段登出時，將會清除該特定MVPD的基礎儲存空間，包括透過該裝置上的SSO取得的所有其他程式設計人員驗證權杖。 將不會刪除為其他MVPD取得或未透過SSO取得的權杖。


## Token {#tokens}

- [定義和使用情況](#definitions)
- [快取准則](#caching)
- [持續性](#persistence)
- [格式](#format)
- [裝置繫結](#device_binding)



### 定義和使用情況 {#definitions}

Primetime驗證軟體權利檔案解決方案圍繞著產生特定資料片段（權杖），Primetime驗證會在成功完成驗證和授權工作流程時產生。 這些權杖會儲存在使用者端的Android裝置上。

權杖的生命週期有限；到期時，需要透過重新初始化驗證和/或授權工作流程重新發行權杖。

在權益工作流程期間會核發三種型別的權杖：

- **驗證Token**  — 使用者驗證工作流程的最終結果將是一個驗證GUID，AccessEnabler可使用它代表使用者進行授權查詢。 此驗證GUID將具有關聯的存留時間(TTL)值，該值可能與使用者的驗證工作階段本身不同。 Primetime驗證會將驗證GUID繫結至起始驗證要求的裝置，藉此產生驗證Token。
- **授權權杖**  — 授予對由唯一識別的特定受保護資源的存取權 `resourceID`. 它由授權方核發的授權授與與原始授權組成 `resourceID`. 此資訊會繫結至起始請求的裝置。
- **短期媒體權杖** - AccessEnabler會傳回短期媒體Token，授與指定資源之託管應用程式的存取權。 此Token是根據先前為該特定資源取得的授權Token而產生。 此外，此代號不會與裝置繫結，而且關聯的生命週期會大幅縮短（預設為： 5分鐘）。

在成功驗證和授權後，Primetime驗證將發佈驗證、授權和短期媒體權杖。 這些權杖應在使用者裝置上快取，並用於其相關生命週期的持續時間。



### 快取准則 {#caching}

- 驗證Token
- 授權Token
- 媒體權杖


#### 驗證Token

- **AccessEnabler 1.6和舊版**  — 驗證權杖在裝置上的快取方式取決於&quot;**每個要求者的驗證」** 與目前MVPD關聯的旗標：


1. 如果「每個請求者的驗證」功能為 *已停用*，則單一驗證Token會儲存在全域作業範圍中的本機。 此代號將在與目前MVPD整合的所有應用程式之間共用。
1. 如果「每個請求者的驗證」功能為 *已啟用*，則權杖會明確與執行驗證流程的程式設計師相關聯（權杖不會儲存在全域作業範圍中，而是儲存在僅供該程式設計師的應用程式看到的私人檔案中）。 更具體來說，將會停用不同應用程式之間的單一登入(SSO)；當切換至新的應用程式時，使用者需要明確執行驗證流程（前提是第二個應用程式的程式設計師已整合至目前的MVPD，而且本機快取中沒有該程式設計師的驗證權杖）。

   **注意：** AE 1.6 Google GSON技術注意事項： [如何解析Gson相依性](https://tve.zendesk.com/entries/22902516-Android-AccessEnabler-1-6-How-to-resolve-Gson-dependencies)

- **AccessEnabler 1.7**  — 此SDK引進了權杖儲存的新方法，可啟用多個程式設計人員 — MVPD貯體，因此可啟用多個驗證權杖。 從AE 1.7開始，「每位請求者的驗證」情況與一般驗證流程都會使用相同的儲存配置。 兩者之間唯一的差異在於執行驗證的方式：「每個請求者的驗證」包含一項新的改進（被動驗證），使AccessEnabler能夠基於儲存體中的驗證權杖存在（針對不同的程式設計人員）執行後端通道驗證。 使用者僅需驗證一次，此工作階段將用於取得後續應用程式中的驗證權杖。 此後端管道流程發生於 [`setRequestor()`](#setRequestor) 呼叫，且對程式設計師來說大部分是透明的。 然而，這裡有一個重要的需求：程式設計師必須呼叫 [`setRequestor()`](#setRequestor) 從主要UI執行緒和活動內。


#### 授權Token

在任何指定時刻，AccessEnabler只會快取每個資源一個授權權杖。 可以快取多個授權權杖，但它們與不同資源相關聯。 每當核發新的授權權杖且同一資源已存在舊授權權杖時，新權杖就會覆寫現有的快取值。



#### 媒體權杖

不應快取短暫的媒體權杖。 每次呼叫授權API時，應該從伺服器擷取媒體權杖，因為它僅限於一次性使用。



### 持續性 {#persistence}

Token必須持續存在於相同應用程式的連續執行中。 這表示取得驗證和授權權杖且使用者關閉應用程式後，當使用者重新開啟應用程式時，應用程式可使用相同的權杖。 此外，這些代號最好在多個應用程式中持續儲存。 換言之，當使用者使用一個應用程式與特定的身分提供者登入（成功取得驗證和授權權杖）後，相同的權杖可以透過不同的應用程式使用，而且當使用者透過相同的身分提供者登入時，不再提示使用者輸入認證。



正是這種流暢的驗證/授權工作流程，使得Primetime驗證解決方案成為真正的電視無處不在的實作。 從純粹的工程觀點來看，Android AccessEnabler程式庫將權杖資料儲存至外部儲存裝置上的資料庫檔案，以解決跨應用程式資料共用問題。 此系統層級的共用資源提供可啟用所需永久權杖使用案例的主要元件：

- 支援結構化儲存 — Primetime驗證Token儲存不僅僅是簡單的線性緩衝記憶體結構。 它提供類似字典的儲存機制，允許根據使用者指定的索引鍵值索引資料。
- 使用基礎檔案系統支援資料持續性 — 預設會儲存資料庫檔案的內容，並將資料儲存在裝置的外部記憶體中。



將特定權杖放入權杖快取中後，AccessEnabler程式庫將在不同時間檢查其有效性。  有效的權杖定義為：

- 權杖的TTL尚未過期
- 權杖的簽發者包含在允許的身分提供者清單中



從AccessEnabler 1.7開始，權杖儲存體可支援多個Programmer-MVPD組合，依賴可容納多個驗證權杖的多層巢狀對應結構。 此新儲存裝置不會以任何方式影響AccessEnabler公用API，而且不需要程式設計師端進行變更。 以下範例說明這項較新的功能：

1. 開啟App1 （由Programmer1開發）。
1. 使用MVPD1 （與程式設計工具1整合）進行驗證。
1. 暫停/關閉目前的應用程式，然後開啟App2 （由Programmer2開發）。
1. 我們假設Programmer2未與MVPD2整合；因此，使用者將不會在App2中驗證。
1. 在App2中使用MVPD2 （已與Programmer2整合）進行驗證。
1. 切換回App1；使用者仍將透過程式設計員1進行驗證。

在舊版AccessEnabler中，步驟6會將使用者呈現為未驗證，因為權杖儲存先前僅支援一個驗證權杖。


**注意：** 從某個程式設計人員/MVPD工作階段登出將會清除基礎儲存空間，包括具有SSO的裝置上的所有其他程式設計人員驗證Token。 將不會刪除為其他MVPD取得或未透過SSO取得的權杖。 取消驗證流程(叫用 [`setSelectedProvider(null)`](#setSelectedProvider))將不會清除基礎儲存體，但只會影響目前的程式設計人員/MVPD驗證嘗試（清除目前程式設計人員的MVPD）。


AccessEnabler 1.7中包含的另一個儲存相關功能可讓您從舊儲存區域匯入驗證權杖。 此「Token Importer」有助於實現連續AccessEnabler版本之間的相容性，即使儲存版本升級時也能維持SSO狀態。

匯入工具會在 [`setRequestor()`](#setRequestor) 流程，並在以下兩種情況下執行（假設目前儲存空間中不存在目前程式設計師的有效驗證Token）：

- 首次安裝由特定程式設計師開發的1.7應用程式
- 升級使用新儲存裝置的未來AccessEnabler路徑

匯入作業對程式設計師而言是透明的，不需要在使用者端應用程式中進行任何程式碼變更。



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

以下清單顯示短媒體權杖的格式。  此Token會公開給程式設計師的應用程式。  在成功的權益程式結束時，它會傳遞給程式設計師的應用程式：

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

在上述XML清單中，請注意標題為 `simpleTokenFingerprint`. 此標籤的用途是儲存原生裝置ID個人化資訊。 AccessEnabler程式庫可取得這類個人化資訊，並在軟體權利檔案呼叫期間提供給Primetime驗證服務。 此服務將使用此資訊並將其嵌入實際權杖，因此可以將權杖有效地繫結到特定裝置。 這的最終目標是要讓權杖不可跨裝置轉讓。



在上述XML清單中，請注意標題為simpleTokenFingerprint的標籤。 此標籤的用途是儲存原生裝置ID個人化資訊。 AccessEnabler程式庫可取得這類個人化資訊，並在軟體權利檔案呼叫期間提供給Primetime驗證服務。 此服務將使用此資訊並將其嵌入實際權杖，因此可以將權杖有效地繫結到特定裝置。 這的最終目標是要讓權杖不可跨裝置轉讓。



由於這顯然是安全性相關功能，因此從安全性觀點來看，此資訊本身就是「敏感」的。 因此，需要保護這些資訊不被竄改和竊聽。 透過透過HTTPS通訊協定傳送驗證/授權請求，即可解決竊聽問題。 處理竄改保護的方法為以數位方式簽署裝置識別資訊。 AccessEnabler程式庫會根據裝置提供的資訊計算裝置ID，然後將裝置ID「以清除形式」傳送至Primetime驗證伺服器，作為要求引數。  Primetime驗證伺服器會使用Adobe的私密金鑰以數位方式簽署裝置ID，並將其新增至傳回至AccessEnabler的驗證權杖。 因此，裝置ID會與驗證Token繫結。  在授權流程期間，AccessEnabler會再次以清除格式傳送裝置ID以及驗證權杖。  驗證程式的失敗將自動導致驗證/授權工作流程失敗。  Primetime驗證伺服器會將私密金鑰套用至裝置ID，並將其與驗證權杖中的值比較。  如果兩者不符，該權益流程就會失敗。


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
