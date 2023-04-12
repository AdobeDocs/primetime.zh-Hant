---
title: MVPD的概觀
description: MVPD的概觀
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# MVPD概述 {#mvpd-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro}

此概觀適用於多管道視訊節目製作經銷商(MVPD)。 有關包括Kickstart和整合指南的其他文檔，請參閱本文檔末尾的「相關資訊」部分。



TVE(TVE)是目前廣為人知的產業運動，可讓付費電視的訂閱者透過多部裝置（不論是在家中或外）存取已付費的內容。  對付費電視供應商而言，TVE創造了新的機會，既可保留現有客戶關係，也可啟用新客戶關係。 然而，隨著這些機遇的到來，挑戰也隨之而來。 在TVE環境中，程式設計人員提供內容，但MVPD保存客戶資訊以驗證潛在觀看者是有效訂閱者。



與一個程式設計師協調查看者身份驗證和授權可能很簡單，但與幾十個或數百個不同的程式設計師協調變得越來越複雜。 但是，有了Adobe® Pass,MVPD只需實施單一、簡單的整合即可進入整個TVE生態系統，包括NBCUniversal Media、Turner Broadcasting(TBS、TNT、CNN)、Fox廣播網路、Hulu等程式設計人員。  Adobe Primetime驗證提供整合架構，讓決定使用者權益變得簡單和安全。



底線：Adobe Primetime驗證可安全地協調程式設計人員與MVPD之間的權限交易，以方便檢視者存取訂閱內容。 換言之，Adobe Primetime驗證可讓適當的客戶輕鬆快速地存取適當的內容。


透過Adobe Primetime驗證，MVPD會收到：

與程式設計人員輕鬆整合。  通過單一整合，從多個內容擁有者提供即時連接。

增強客戶互動。  支援流暢的品牌化體驗，因為您的客戶可跨多個平台和裝置檢視內容。

安全驗證。  確保僅授權的使用者和裝置有權存取優質內容，並（選擇性）限制每個家庭帳戶可連線的裝置和同時串流的數量。

## 常見問題集 {#faq}

Adobe Primetime驗證的安全性為何？ Adobe Primetime驗證架構的第一優先順序是確保只有經過授權的檢視者才能驗證，且能存取優質內容。 Adobe Primetime驗證可將檢視裝置的存取權緊密系結，並有助於限制指定家庭的資料流、工作階段和/或裝置。


需要Flash Player嗎？ Adobe Primetime TV Everywhere驗證不受播放器和平台限制，可與任何播放應用程式整合，包括Silverlight和HTML5。 此外，Adobe Primetime驗證也針對執行iOS和Android的手機和平板電腦等裝置提供原生支援。


Adobe Primetime驗證支援哪些裝置？ Adobe Primetime驗證幾乎受到任何具備HTML5網頁套件的裝置所支援，以提供瀏覽器內檢視體驗。 此外，Adobe Primetime驗證仍在針對各種裝置特定平台推出原生軟體開發套件(SDK)，包括iOS、Android™、Xbox360（已淘汰）和AdobeAir®（已淘汰）應用程式。 最近，Adobe Primetime驗證針對無法轉譯瀏覽器頁面的裝置（例如「智慧型」電視、電視盒和遊戲主機）推出無用戶端解決方案。  使用MVPD驗證使用者時，必須具備演算瀏覽器頁面的功能。


Adobe Primetime驗證是否支援Tv Everywhere的新興標準？ Adobe Primetime驗證符合CableLabs OLCA（線上內容存取）規格，該規格提供從線上來源傳送視訊給付費電視客戶的技術需求和架構。 Adobe於2011年6月參與CableLabs整合測試專案，並通過服務提供者實作的測試程式。 Adobe Primetime驗證會根據OLCA規範進行驗證（完整且測試）。 授權元件已完成，但測試驗證當前正在等待CableLabs測試環境的發佈。 Adobe還是OATC（開放認證技術聯合會）的積極成員，作為該機構的一部分，參與了幾個小組委員會的規範起草項目。



什麼是驗證？ 驗證是MVPD確認指定的使用者為已知客戶的程式。



什麼是授權？ 授權是MVPD確認已驗證的用戶對給定資源具有有效訂閱的過程。



## 架構 {#architecture}

Adobe Primetime驗證是托管服務，可根據MVPD和程式設計人員所需的業務規則，允許快速後端（伺服器對伺服器）整合。 這意味著可以快速向所有交易方營銷、更安全的防欺詐環境，以及更出色的客戶體驗，讓更多的電視內容可供更多平台上的更多用戶使用。


Adobe Primetime驗證是透過軟體即服務(SaaS)模型提供，並可讓使用者、MVPD和程式設計人員之間進行更安全的通訊，以驗證內容的權限。 服務的核心元件包括：

伺服器端 — 托管的Adobe Primetime驗證伺服器。 這是一個應用伺服器，用於與MVPD的驗證系統進行後通道（伺服器對伺服器）通信。
用戶端：客戶端Access Enabler - Access Enabler是一個小檔案，載入到程式設計師的網頁或播放器應用程式中。 它為程式設計師的內容查看應用程式提供權限API，並與Adobe Primetime驗證伺服器通信。
無用戶端Web服務（適用於非Web功能的裝置） — 為智慧型電視、遊戲主機和機上盒等裝置提供權限API的RESTful Web服務。

>[!NOTE]
>
>身為MVPD，您的網站服務必須能夠識別Adobe Primetime驗證的驗證和授權要求，並以預期格式回應所需資料。

Adobe Primetime驗證可讓您為客戶提供同盟身分管理，也稱為單一登入(SSO)驗證和授權。 使用Adobe Primetime驗證時，只要MVPD允許保留該驗證，訂閱者就不需要在第一次驗證後重新登入。 （通常為30天。） 為達此目的，Adobe Primetime驗證為客戶提供驗證Token的通用網域。 與指定MVPD整合的所有參與網站都可使用此驗證狀態資訊。


目前，大部分與MVPD的Adobe Primetime驗證整合都使用SAML通訊協定，這是主要驗證標準之一。 Adobe Primetime驗證在SAML架構中充當代理服務提供者，並將SAML驗證回應保存為Adobe公用網域中的安全Token。 Adobe Primetime驗證符合SAML 2.0。 不過，雖然Adobe Primetime驗證目前通常與SAML SSO解決方案搭配使用，但Adobe Primetime驗證架構並未系結至任何特定通訊協定。 因此，新通訊協定（例如以OAuth 2.0為基礎的通訊協定或自訂通訊協定）的支援可隨著時間而增加。


Adobe會與MVPD的技術團隊合作，設定Adobe Primetime驗證以符合任何現有整合的需求。 假設整合為「標準」且最低支援需求（檔案和基本電子郵件支援）,MVPD的整合是免費的。 如果MVPD需要重大支援或時間表升級，則可能需要支付支援費，或者提供者可能希望與熟悉我們解決方案的第三方（如Syncor）合作。


Adobe Primetime驗證也支援有效處理MVPD業務邏輯，如下所示：

對於自包含的業務邏輯，當接收到授權請求時可由MVPD應用，當MVPD接收到授權請求時，Adobe提供支援業務邏輯執行所需的必要資料。 此資料可包含但不限於提出請求的使用者的唯一裝置ID，以及裝置的IP位址。

對於需要使用者干預和/或由Adobe解決方案特定處理的業務邏輯，Adobe可以維護每個MVPD的某些自訂屬性。 這些MVPD專屬的設定/原則包括啟用預先定義的工作流程，這些工作流程可在頂層工作流程的特定時間點啟動。 如需自訂屬性支援的詳細資訊，請連絡您的Adobe代表。

下圖說明MVPD和程式設計師與這些Adobe Primetime驗證元件的關係：

![](assets/high-level-architecture-nflows.png)

*圖：高階架構和流程*

## Adobe Primetime驗證元件 {#components}

以下概述Adobe Primetime驗證生態系統的部分主要元件。 這些包括：

* [Access Enabler /無客戶端Web服務](#ae)
* [Adobe托管的後端伺服器](#backend)
* [代號](#tokens)

### Access Enabler /無客戶端Web服務 {#ae}

Access Enabler可促進與用戶的所有身份驗證和授權交互，並在用戶的系統上本地運行。 它是Access Enabler，它使用MVPD處理實際權限工作流，而程式設計師則負責更高級的網頁或播放器應用。

Adobe Primetime會為無法呈現網頁的裝置提供無用戶端Web服務。  對於這些裝置，授權程式會在智慧裝置上啟動和檢視內容，而具有MVPD的驗證會在可上網的裝置（PC、智慧手機和平板電腦）上進行。

Access Enabler :

* 啟動MVPD專屬驗證和授權工作流程。
* 對每個程式設計師資源/通道的成功授權響應進行快取以最大限度地減少不必要的請求流量。
* 可針對每個MVPD專屬的預先定義工作流程進行設定，例如明確的裝置註冊。
* 可透過下清單格取得：
   * SWF檔案，Flash Player執行階段可執行
   * 由瀏覽器直接執行的JS檔案
   * 適用於各種平台(包括iOS、Android和Xbox)的本機Access Enabler。

### Adobe托管後端伺服器 {#backend}

Adobe Primetime驗證後端伺服器，由Adobe托管：

* 使用需要Adobe Primetime驗證與運算子之間伺服器對伺服器通訊的MVPD來設定驗證和授權工作流程。
* 維護程式設計師站點和應用程式的配置。
* 托管可下載的Access Enabler元件檔案。
* 產生驗證和授權Token。

### 代號 {#tokens}

Adobe Primetime驗證權限解決方案以產生在成功完成驗證/授權工作流程時所取得的特定資料片段為中心。 這些資料片段稱為代號。 它們的有效期有限，並且安全地儲存在與平台相關的位置中。 到期時，必須透過重新啟動驗證和/或授權工作流程來重新核發權杖。

驗證/授權工作流程期間會發出三種代號。 其中兩個是「長期」的，提供了用戶觀看體驗的連續性。 第三種是短期代號，支援通過流剝離來減輕欺詐的行業最佳做法。 代號的存留時間(「TTL」)值是根據MVPD與程式設計人員之間的協定來設定。 您可以決定最符合企業和客戶需求的TTL值。

**長期驗證權杖**. 客戶使用Adobe Primetime驗證成功登入其MVPD帳戶後，驗證就會成功。 Adobe Primetime驗證接著會產生與要求裝置系結的長期驗證(「authN」)代號，以及（視MVPD而定）匿名識別使用者的全域唯一識別碼(「GUID」)。

**長期使用的授權代號**. 成功授權後，Adobe Primetime驗證會建立長期授權(「authZ」)代號。 此代號無法攜帶，因為它已系結至請求裝置和特定保護資源（例如頻道、系列或集數）。 Access Enabler使用長壽命authZ令牌建立用於實際查看訪問的短壽命媒體令牌。

**短暫的媒體代號**. 授權使用者後，Adobe Primetime驗證會產生authZ代號，並使用該代號產生由Adobe簽署並加密的單一用途、短期的媒體代號，以避免交換期間遭到篡改。 由於短期令牌是通過Access Enabler API或無客戶端Web服務向嵌入站點公開的，因此在提供對受保護資源的訪問之前，程式設計師的媒體伺服器必須使用Adobe Primetime驗證元件（媒體令牌驗證器）來驗證令牌。

## MVPD整合生命週期 {#lifecycle}

下圖顯示Adobe Primetime驗證和MVPD之間整合的生命週期。

![](assets/mvpd-int-lifecycle.png)

*圖：MVPD整合生命週期*

## 權利流程圖 {#chart}

以下流程圖說明使用Adobe Primetime驗證確認權限的整體程式：

![](assets/authn-authz-entitlmnt-flow.png)

*圖：使用Adobe Primetime驗證確認權限的程式*

## 驗證步驟 {#authn-steps}

下列步驟提供Adobe Primetime驗證流程的範例。  這是權限流程的一部分，程式設計師在該流程中確定用戶是否是MVPD的有效客戶。  在此案例中，使用者是MVPD的有效訂閱者。  用戶正嘗試使用程式設計師的Flash應用程式查看受保護的內容：

1. 用戶瀏覽到程式設計師的網頁，該網頁將程式設計師的Flash應用程式和Adobe Primetime身份驗證Access Enabler元件載入到用戶的電腦上。 Flash應用程式使用Access Enabler將程式設計師的標識設定為Adobe Primetime身份驗證，而Adobe Primetime身份驗證將Access Enabler的配置和狀態資料作為該程式設計師（「請求者」）的優先順序。 Access Enabler必須先從伺服器接收此資料，然後才能執行任何其他API調用。  技術說明：程式設計師使用Access Enabler設定其身份 `setRequestor()` 方法；如需詳細資訊，請參閱 [程式設計師整合指南](/help/authentication/programmer-integration-guide-overview.md).
1. 當用戶嘗試查看程式設計師的受保護內容時，程式設計師的應用程式向用戶提供MVPD清單，用戶從中選擇提供者。
1. 系統會將使用者重新導向至Adobe Primetime驗證伺服器，在此伺服器中會建立使用者選取之MVPD的加密SAML要求。 此請求以代表程式設計師的身份驗證請求的形式發送到MVPD。 根據MVPD的系統，然後將用戶的瀏覽器重定向到MVPD的站點以登錄，或在程式設計師的應用中建立登錄iFrame。
1. 在任何情況下（重新導向或iFrame）,MVPD都會接受請求並顯示其登入頁面。
1. 使用者透過MVPD登入，MVPD會驗證使用者付費客戶的狀態，然後MVPD會建立自己的HTTP工作階段。
1. 驗證使用者後，MVPD會建立回應（SAML和加密）,MVPD會將回應傳回Adobe Primetime驗證。
1. Adobe Primetime驗證會接收MVPD回應，看到有Adobe Primetime驗證HTTP工作階段已開啟，會驗證 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 從MVPD響應，並重新定向回程式設計員站點。
1. 重新載入程式設計師的站點，重新載入Access Enabler，並再次調用setRequestor()。  由於當前配置已更改，對setRequestor()的第二個調用是必需的 — 現在存在一個標誌，它通知Access Enabler伺服器上正在等待生成AuthN令牌。
1. Access Enabler發現有掛起的身份驗證，並從Adobe Primetime身份驗證伺服器請求令牌。 通過調用Flash Player的DRM功能從伺服器中檢索令牌。
1. AuthN令牌儲存在程式設計師的Flash PlayerLSO快取中；驗證現已完成，且工作階段會在Adobe Primetime驗證伺服器上銷毀。

## 授權步驟 {#authz-steps}

從上一節繼續下列步驟([驗證步驟](#authn-steps)):

1. 當用戶嘗試訪問程式設計師保護的內容時，程式設計師的應用程式首先檢查用戶的本地電腦或設備上是否有AuthN令牌。  如果代號不在，則 [驗證步驟](#authn-steps) 以上項目。  如果AuthN令牌存在，則授權流程將隨程式設計師的應用程式啟動對Access Enabler的調用，請求獲取用戶對受保護內容的特定項目的查看權限。
1. 受保護內容的特定項由「資源標識符」表示。  這可以是簡單的字串或更複雜的結構，但無論如何，資源標識符的性質是事先在程式設計師和MVPD之間商定的。  程式設計師的應用程式將資源標識符傳遞給Access Enabler。  Access Enabler會檢查用戶的本地電腦或設備上是否有AuthZ令牌。  如果AuthZ代號不存在，Access Enabler會將請求傳遞至後端Adobe Primetime驗證伺服器。
1. Adobe Primetime驗證伺服器使用標準化通訊協定與MVPD授權端點通訊。  如果MVPD的回應指出使用者有權檢視受保護的內容，Adobe Primetime驗證伺服器會建立AuthZ權杖，並傳回給存取啟用碼，該啟用碼會將AuthZ權杖儲存在使用者的電腦上。
1. 在用戶的機器或設備上儲存AuthZ令牌後，程式設計師的應用程式調用Access Enabler從Adobe Primetime驗證伺服器獲取媒體令牌，並將該令牌提供給程式設計師的應用程式。
1. 最後，程式設計師的應用程式使用媒體令牌驗證器元件來確認正確的用戶正在查看正確的內容，並且在設定了媒體令牌後，允許用戶查看受保護的內容。

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
