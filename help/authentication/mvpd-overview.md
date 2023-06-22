---
title: MVPD概述
description: MVPD概述
exl-id: b918550b-96a8-4e80-af28-0a2f63a02396
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---

# MVPD概述 {#mvpd-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#intro}

本概述適用於多頻道視訊節目經銷商(MVPD)。 如需其他檔案，包括Kickstart和整合指南，請參閱本檔案結尾的「相關資訊」一節。



TV Everywhere (TVE)是現在廣為人知的產業運動，它讓Pay TV的訂閱者能夠跨多部裝置存取他們已經在家中的付費內容。  對於付費電視供應商，TVE會建立新的商機，以保留現有的客戶關係並啟用新的客戶關係。 然而，這些機遇伴隨著挑戰。 在TVE環境中，程式設計師會提供內容，但MVPD會儲存客戶資訊，以驗證潛在檢視者是有效的訂閱者。



與一名程式設計師協調檢視者驗證和授權可能很簡單，但與數十或數百名不同程式設計師的協調卻變得越來越複雜。 然而，透過Adobe® Pass，MVPD只需要實作單一、簡單的整合，即可存取整個TVE生態系統，包括NBC環球媒體、Turner Broadcasting (TBS、TNT、CNN)、Fox Broadcast Networks、Hulu等程式設計師。  Adobe Primetime驗證提供整合架構，可讓您輕鬆安全地判斷使用者軟體權利檔案。



要點： Adobe Primetime驗證可安全地協調程式設計師和MVPD之間的授權交易，方便檢視者存取訂閱內容。 換句話說，Adobe Primetime驗證可讓適當的客戶輕鬆快速地存取適當的內容。


透過Adobe Primetime驗證，MVPD會接收：

與程式設計師輕鬆整合。  透過單一整合，提供來自多個內容擁有者的即時連線能力。

增強客戶參與度。  當客戶檢視多個平台和裝置上的內容時，支援順暢的品牌體驗。

安全驗證。  確保只有授權的使用者和裝置才能存取進階內容，並（選擇性）限制每個家庭帳戶可連線的裝置和同時串流數量。

## 常見問題集 {#faq}

Adobe Primetime驗證的安全性如何？ Adobe Primetime驗證架構的第一要務是確保僅授權檢視者通過驗證，並獲授權存取進階內容。 Adobe Primetime驗證會將存取許可權緊密繫結到檢視裝置，並可協助限制特定家庭的串流、工作階段和/或裝置。


是否需要Flash Player？ 適用於TV Everywhere的Adobe Primetime驗證不受播放器和平台限制，可與任何播放應用程式(包括Silverlight和HTML5)整合。 此外，Adobe Primetime驗證還為執行iOS和Android的手機和平板電腦等裝置提供原生支援。


Adobe Primetime驗證支援哪些裝置？ 幾乎任何具備HTML5 Web套件且提供瀏覽器內檢視體驗的裝置皆支援Adobe Primetime驗證。 此外，Adobe Primetime驗證繼續針對各種裝置特定平台推出原生軟體開發套件(SDK)，包括iOS、Android™、Xbox360 （已棄用）和Adobe Air® （已棄用）應用程式。 最近，Adobe Primetime驗證推出無使用者端解決方案，適用於無法轉譯瀏覽器頁面的裝置（例如「智慧」電視、機上盒和遊戲主機）。  使用MVPD驗證使用者時，需要具備轉譯瀏覽器頁面的能力。


Adobe Primetime驗證是否支援各地電視的新興標準？ Adobe Primetime驗證符合CableLabs OLCA （線上內容存取）規格，該規格提供從線上來源將視訊傳送給付費電視客戶的技術需求和架構。 Adobe於2011年6月參與了CableLabs的聯合Interopt測試專案，並通過了服務供應商實作的測試程式。 Adobe Primetime驗證會根據OLCA的驗證規格進行驗證（完整和測試）。 授權元件已完成，但測試驗證目前等待CableLabs測試環境發佈。 Adobe也是OATC （開放式驗證技術聯盟）的積極成員，並參與了該機構的幾個小組委員會規格起草專案。



什麼是驗證？ 驗證是MVPD確認指定使用者為已知客戶的程式。



什麼是授權？ Authorization是MVPD確認已驗證的使用者是否擁有指定資源的有效訂閱的程式。



## 架構 {#architecture}

Adobe Primetime驗證是一項託管服務，可根據MVPD和程式設計師所需的商業規則，進行快速後端（伺服器對伺服器）整合。 這表示所有各方都能快速上市、提供更安全的環境以防止欺詐，以及卓越的客戶體驗，讓更多平台上的更多人能看到更多的電視內容。


Adobe Primetime驗證透過軟體即服務(SaaS)模式提供，並可讓一般使用者、MVPD和程式設計師之間進行更安全的通訊，以驗證內容的權益。 服務的核心元件包括：

伺服器端 — 託管的Adobe Primetime驗證伺服器。 這是應用程式伺服器，可與MVPD的驗證系統進行後端通道（伺服器對伺服器）通訊。
使用者端：使用者端Access Enabler - Access Enabler是載入程式設計師網頁或播放器應用程式中的小型檔案。 它為程式設計師的內容檢視應用程式提供權益API，並與Adobe Primetime驗證伺服器通訊。
無使用者端網頁服務（適用於不支援網頁的裝置） - RESTful網頁服務，為智慧型電視、遊戲主機和機上盒等裝置提供軟體授權API。

>[!NOTE]
>
>身為MVPD，您的Web服務必須能夠識別來自Adobe Primetime驗證的驗證和授權請求，並以預期格式回應所需的資料。

Adobe Primetime驗證可讓您為客戶提供同盟身分管理，也稱為單一登入(SSO)驗證和授權。 使用Adobe Primetime驗證時，只要MVPD允許保留該驗證，訂閱者就不需要在第一次驗證後再次登入。 （通常為30天。） 為了完成此操作，Adobe Primetime驗證會為我們的客戶提供驗證權杖的共同網域。 與特定MVPD整合的所有參與網站都可以使用此驗證狀態資訊。


目前，大部分的Adobe Primetime驗證與MVPD整合都使用SAML通訊協定，這是主要驗證標準之一。 Adobe Primetime驗證會成為SAML架構中的Proxy服務提供者，並將SAML驗證回應儲存為Adobe通用網域中的安全權杖。 Adobe Primetime驗證符合SAML 2.0規範。 不過，雖然Adobe Primetime驗證目前通常與SAML SSO解決方案搭配使用，但Adobe Primetime驗證架構未繫結到任何特定通訊協定。 因此，可以隨著時間新增對新通訊協定的支援，例如基於OAuth 2.0或自訂通訊協定的支援。


Adobe會與MVPD的技術團隊合作，設定Adobe Primetime驗證，以滿足任何現有整合的需求。 MVPD可免費整合，且須具備「標準」整合及最低支援需求（檔案和基本電子郵件支援）。 如果MVPD需要大量支援或升級的時間表，可能需要支付支援費用，或提供者可能想要與熟悉我們的解決方案的協力廠商合作，例如Synacor。


Adobe Primetime驗證也支援有效處理MVPD商業邏輯，如下所示：

對於獨立且可在收到授權請求時由MVPD套用的商業邏輯，Adobe會在MVPD收到授權請求時提供支援商業邏輯執行所需的必要資料。 此資料可以包括但不限於提出請求之使用者的唯一裝置ID和裝置的IP位址。

對於需要使用者介入和/或Adobe解決方案特定處理的商業邏輯，Adobe可以維護每個MVPD的一些自訂屬性。 這些MVPD特定設定/原則包括啟用預先定義的工作流程，這些工作流程可以在頂層工作流程的特定時間點啟動。 如需自訂屬性支援的詳細資訊，請聯絡您的Adobe代表。

下圖說明MVPD和程式設計師與這些Adobe Primetime驗證元件的關係：

![](assets/high-level-architecture-nflows.png)

*圖：高階架構和流程*

## Adobe Primetime驗證元件 {#components}

以下提供Adobe Primetime驗證生態系統的部分主要元件概觀。 其中包括：

* [存取啟用程式/無使用者端Web服務](#ae)
* [Adobe託管後端伺服器](#backend)
* [Token](#tokens)

### Access Enabler/無使用者端Web服務 {#ae}

Access Enabler可促進與使用者的所有驗證和授權互動，並在其系統上本機執行。 它是Access Enabler，會使用MVPD處理實際權益工作流程，而程式設計師則負責處理較高層級的網頁或播放器應用程式。

Adobe Primetime驗證為無法轉譯網頁的裝置提供無使用者端網頁服務。  對於這些裝置，軟體權利檔案程式會在智慧型裝置上啟動，且內容會在智慧型裝置上檢視，而使用MVPD的驗證則會發生在支援網頁的裝置（PC、智慧型手機和平板電腦）上。

存取啟用碼：

* 啟動MVPD特定的驗證和授權工作流程。
* 根據程式設計人員資源/通道快取成功的授權回應，以減少不必要的請求流量。
* 可針對每個MVPD特定的預先定義工作流程進行設定，例如明確裝置註冊。
* 提供下列格式：
   * Flash Player執行階段可執行的SWF檔案
   * 由瀏覽器直接執行的JS檔案
   * 適用於各種平台(包括iOS、Android和Xbox)的原生Access Enabler。

### Adobe裝載的後端伺服器 {#backend}

Adobe Primetime驗證後端伺服器，由Adobe託管：

* 布建驗證和授權工作流程與需要Adobe Primetime驗證和操作員之間伺服器對伺服器通訊的MVPD。
* 維護程式設計師網站和應用程式的設定。
* 裝載可下載的Access Enabler元件檔案。
* 產生驗證和授權權杖。

### Token {#tokens}

Adobe Primetime驗證權利解決方案的中心，是產生特定資料片段，這些片段會在成功完成驗證/授權工作流程後取得。 這些資料片段稱為Token。 這類檔案存留期有限，且會安全地儲存在平台相關位置。 到期後，必須透過重新起始驗證和/或授權工作流程重新核發權杖。

在驗證/授權工作流程期間會核發三種型別的權杖。 其中兩個是「長期」的，可提供使用者觀看體驗的連續性。 第三個是短效代號，可支援業界最佳實務，以透過串流擷取來減少詐騙。 權杖的存留時間(「TTL」)值是根據MVPD和程式設計師之間的協定來設定。 您可以決定最適合您的企業和客戶的TTL值。

**長效驗證權杖**. 客戶使用Adobe Primetime驗證成功登入其MVPD帳戶後，驗證就會成功。 Adobe Primetime驗證接著會產生與請求裝置繫結的長期驗證(「authN」)權杖，以及（根據MVPD）可匿名識別使用者的全域唯一識別碼(「GUID」)。

**長效授權權杖**. 在成功授權後，Adobe Primetime驗證會建立長效授權(「authZ」)權杖。 此權杖無法攜帶，因為它繫結至請求裝置和特定的受保護資源（例如頻道、影集或集數）。 Access Enabler會使用長效的authZ權杖，建立用於實際檢視存取權的短效媒體權杖。

**短期媒體代號**. 使用者獲得授權後，Adobe Primetime驗證會產生authZ權杖，並使用該權杖產生一次性使用的短期媒體權杖，並由Adobe簽署及加密，以避免在交換期間遭到竄改。 因為短期權杖會透過Access Enabler API或無使用者端Web服務向內嵌網站公開，在提供受保護資源的存取權之前，程式設計師的媒體伺服器必須使用Adobe Primetime驗證元件（媒體權杖驗證器）來驗證權杖。

## MVPD整合生命週期 {#lifecycle}

下圖顯示Adobe Primetime驗證和MVPD之間整合的生命週期。

![](assets/mvpd-int-lifecycle.png)

*圖： MVPD整合生命週期*

## 權利流程圖 {#chart}

以下流程圖顯示使用Adobe Primetime驗證確認軟體權利檔案的整體程式：

![](assets/authn-authz-entitlmnt-flow.png)

*圖：使用Adobe Primetime驗證確認權益的程式*

## 驗證步驟 {#authn-steps}

下列步驟提供Adobe Primetime驗證流程的範例。  這是軟體權利檔案程式的一部分，程式設計師在其中判斷使用者是否為MVPD的有效客戶。  在此案例中，使用者是MVPD的有效訂閱者。  使用者正嘗試使用程式設計師的Flash應用程式檢視受保護的內容：

1. 使用者瀏覽到程式設計人員的網頁，該網頁會將程式設計人員的Flash應用程式和Adobe Primetime驗證Access Enabler元件載入到使用者的電腦上。 Flash應用程式會使用Access Enabler來設定程式設計師的識別碼並進行Adobe Primetime驗證，而Adobe Primetime驗證會為該程式設計師（「請求者」）的設定和狀態資料啟動Access Enabler。 Access Enabler必須先從伺服器接收此資料，才能執行任何其他API呼叫。  技術說明：程式設計師使用Access Enabler的 `setRequestor()` 方法；如需詳細資訊，請參閱 [程式設計師整合指南](/help/authentication/programmer-integration-guide-overview.md).
1. 當使用者嘗試檢視程式設計師的受保護內容時，程式設計師的應用程式會向使用者顯示MVPD清單，使用者可從中選擇提供者。
1. 系統會將使用者重新導向至Adobe Primetime驗證伺服器，其中會建立使用者所選MVPD的加密SAML要求。 此要求會以代表程式設計師的驗證要求形式傳送至MVPD。 根據MVPD的系統，使用者的瀏覽器會被重新導向至MVPD的網站以登入，或在程式設計人員的應用程式中建立登入iFrame。
1. 無論是哪種情況（重新導向或iFrame），MVPD都會接受要求並顯示其登入頁面。
1. 使用者使用MVPD登入，MVPD會驗證使用者作為付款客戶的狀態，然後MVPD會建立自己的HTTP工作階段。
1. 驗證使用者後，MVPD會建立回應（SAML和加密），然後MVPD會將其傳回Adobe Primetime驗證。
1. Adobe Primetime驗證會收到MVPD回應，看到有Adobe Primetime驗證HTTP工作階段開啟，並驗證 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 會從MVPD回應，並重新導向回程式設計師的網站。
1. 程式設計師的網站會重新載入、存取啟用碼會重新載入，而程式設計師會再次呼叫setRequestor()。  需要對setRequestor()進行第二次呼叫，因為目前的設定已變更 — 現在出現一個旗標，通知Access Enabler伺服器上正在等待產生AuthN權杖。
1. Access Enabler發現擱置中的驗證，並向Adobe Primetime驗證伺服器要求Token。 Token是透過叫用Flash Player的DRM功能從伺服器擷取。
1. AuthN權杖儲存在程式設計師的Flash PlayerLSO快取中；驗證現在已完成，且工作階段已在Adobe Primetime驗證伺服器上毀損。

## 授權步驟 {#authz-steps}

以下步驟延續前一節的內容([驗證步驟](#authn-steps))：

1. 當使用者嘗試存取程式設計師的受保護內容時，程式設計師的應用程式會先檢查使用者本機電腦或裝置上的AuthN權杖。  如果該Token不存在，則 [驗證步驟](#authn-steps) 以上說明如下。  如果有AuthN權杖，授權流程會隨著程式設計師的應用程式繼續進行，起始對存取啟用程式的呼叫，並要求取得使用者對受保護內容的特定專案的檢視許可權。
1. 受保護內容的特定專案由「資源識別碼」表示。  這可以是簡單的字串或更複雜的結構，但在任何情況下，資源識別碼的性質都能在程式設計師和MVPD之間事先商定。  程式設計師的應用程式會將資源識別碼傳遞給Access Enabler。  Access Enabler會檢查使用者的本機電腦或裝置上的AuthZ權杖。  如果沒有AuthZ權杖，Access Enabler會將要求傳遞至後端Adobe Primetime驗證伺服器。
1. Adobe Primetime驗證伺服器使用標準化的通訊協定與MVPDs授權端點通訊。  如果MVPD的回應指出使用者有權檢視受保護的內容，則Adobe Primetime驗證伺服器會建立AuthZ權杖，並將其傳回Access Enabler，後者會將AuthZ權杖儲存在使用者的電腦上。
1. 將AuthZ權杖儲存在使用者的電腦或裝置上，程式設計師的應用程式會呼叫Access Enabler以從Adobe Primetime驗證伺服器取得媒體權杖，並將該權杖提供給程式設計師的應用程式。
1. 最後，程式設計師的應用程式會使用媒體權杖驗證器元件，以確認正確的使用者正在檢視正確的內容，並且在媒體權杖就緒後，允許使用者檢視受保護的內容。

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
