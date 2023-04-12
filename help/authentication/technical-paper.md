---
title: 關於Adobe Primetime驗證和TV Everywhere
description: 關於Adobe Primetime驗證和TV Everywhere
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '6288'
ht-degree: 0%

---


# 關於Adobe Primetime驗證和TV Everywhere {#about-auth-tve}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 關於TV Everywhere {#about-tve}

如今的電視觀眾可以隨時或地點上網，他們希望他們能夠隨身訪問付費電視內容。 此外，受眾正在使用不斷增加的支援網際網路的設備查看內容，包括：

* 筆記型電腦
* 平板電腦
* 智慧手機
* 網站
* 同盟應用程式
* 遊戲機
* 機頂盒
* 智慧型電視

TV Everywhere是業界運動，它支援付費電視訂閱者在家中和家外的多部裝置上，存取他們已付費的內容。 儘管大部分電視觀看仍發生在傳統的線性電視上，但消費的增長是時移內容、線上視頻和替代螢幕。 因此，當今的視頻發佈市場處於中斷狀態，而TV Everywhere已成為符合程式設計師、付費電視提供商和付費電視訂戶利益的解決方案。


TV Everywhere的技術目標是使付費電視客戶能夠訪問他們已在其所有設備和平台上訂閱的內容。


TV Everywhere的業務目標是：

* **保留現有客戶關係並啟用新客戶關係**
* 允許程式設計師和內容擁有者觸及最廣的受眾，並從優質內容中獲取更多價值
* 透過與檢視者的直接線上互動來擴充品牌

## TV Everywhere挑戰 {#tve-challenges}

隨著TV Everywhere的機遇，挑戰也隨之而來。 這些的核心是權利。 在檢視器存取訂閱內容之前，必須先由某人判斷他們是否有權存取該訂閱內容。

使用者是否有付費電視提供者的訂閱？ 如果是，該訂閱是否包含正在請求的內容？ 權利對於程式設計師和內容所有者來說尤其難以直接確定，因為付費電視運營商擁有其客戶的標識資料以及其客戶的訪問權限。


除應享權利外，還有一系列相關的技術和整合挑戰，包括：

* 制定和實施全面的多設備戰略
* 協調程式設計師與付費電視提供商之間的眾多關係
* 防止欺詐性訪問或濫用服務條款
* 為跨網站和應用程式的使用者提供一致且無挫折的驗證體驗
* 維護快速上市時間以跟上附屬機構交易
* 管理與多項整合相關的成本

這些難題使程式設計師與多個付費電視提供商的驗證系統之間的執行和維護複雜、直接的整合非常耗用資源，需要時間和技術複雜性。


解決方案？ **Adobe® Primetime驗證**.

## Adobe Primetime驗證簡介 {#authentication-intro}

透過Adobe Primetime驗證，程式設計人員和付費電視提供者只需執行簡單的整合，使用Adobe Primetime驗證API即可存取整個生態系統，包括：

* 特納廣播(TBS、TNT、CNN)、福克斯廣播網和葫蘆網等程式設計師

* 美國所有頂級付費電視提供商，佔美國所有付費電視家庭的90%以上

此外，Adobe Primetime驗證提供的架構讓使用者驗證和授權簡單且安全。

![](assets/programmers-connect-authn.png)

*圖1:只有一些程式設計師和付費電視提供商通過Adobe Primetime驗證連接……*

Adobe Pass安全地協調程式設計師與付費電視提供者之間的權利交易，方便檢視者存取訂閱內容。 換句話說……

**Adobe Primetime驗證可讓適當的客戶輕鬆快速地存取適當的內容。**

**Adobe Primetime驗證的對象是誰？**

* **程式設計師** 想要輕鬆與付費電視提供者（也稱為「MVPD」或「多頻道視訊程式設計經銷商」）整合，並觸及最廣的受眾，以獲得最佳收入。 使用Adobe Primetime驗證，程式設計人員可以驗證所有主要提供者的檢視器，不受用戶端平台影響。

* **付費電視提供者/MVPD** 通過方便線上訪問訂閱內容，尋求與多個程式設計師無痛的連接，並提高客戶滿意度。

* **付費電視客戶** 想要輕鬆存取已訂閱內容（無論在何處）的使用者，不需額外付費。 單一登入可在網路或行動應用程式間提供安全的檢視器驗證，而不需要用戶端下載或重複登入，並提供良好的使用者體驗。

針對 **程式設計師**,Adobe Primetime驗證提供：

* 與頂級付費電視提供者輕鬆整合及立即連線，無需進行多次直接整合
* 透過支援最廣的內容受眾，最佳化訂閱（授權）和廣告收入
* 安全驗證，只授予授權用戶/設備對高級內容的訪問權
* 開放且靈活的架構，不受播放器和DRM平台限制；播放可在多種平台上進行，包括iOS、Android、Windows 8、遊戲主控台、機上盒等。
* 與任何DRM技術相容，例如AdobeFlash Access®或播放就緒®。
* 支援單一登入(SSO)驗證和授權，因此訂閱者在其自己的系統上首次驗證後，不需要再次登入。


針對 **付費電視提供者/MVPD**,Adobe Primetime驗證提供：

* 與內容所有者輕鬆整合，使用單一整合提供與多個程式設計師的即時連接
* 透過支援跨多個平台和裝置檢視內容的流暢、品牌化體驗，增強客戶參與度
* 安全驗證，可確保只有授權的使用者/裝置才能存取優質內容，並（可選）限制每個家庭帳戶可連線的裝置數和同時串流。


針對 **付費電視客戶**,Adobe Primetime驗證提供：

* **TV Everywhere!**

本文的其餘部分將介紹Adobe Primetime身份驗證的技術。  雖然以下大部分內容側重於程式設計師整合，但還有適用於付費電視提供商的一般資訊和特定資訊。 本檔案也重點說明Adobe Primetime驗證作為TV Everywhere解決方案時的安全性與完整性。 欲知本白皮書之外的更多詳細資訊，請聯繫您的Adobe代表或填寫「資訊請求」表 [此處](https://www.adobe.com/).

## 建築構築 {#arch-building-blocks}

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/import-pc7mz3dfnv/check.gif) 下面討論了身份驗證和授權的中央權利事務。 驗證是向付費電視提供者確認特定使用者為已知客戶的程式。 授權是付費電視提供者確認已驗證的使用者對指定資源有效訂閱的程式。
Adobe Primetime驗證包含下列基本元件：

* 用戶端元件（下列其中一項）:

   * Access Enabler — 特定於平台的庫；提供簡單易用的API和程式碼範例，以實作權限流程
   * 無客戶端API - RESTful Web服務；為不具網頁呈現功能（例如遊戲主控台、機上盒等）的平台提供權限流程端點

* Adobe托管後端伺服器
* 媒體代號驗證器
* 安全的中央交換媒體（代號）

在基本層級，Adobe Primetime驗證包含三個元件(Access Enabler、Adobe托管的後端伺服器和媒體令牌驗證器)和一個中央交換項（令牌）。

### 用戶端元件 {#client-components}

* Access Enabler
* 無用戶端API

#### Access Enabler {#access-enabler}

在完全支援的平台(包括Web、iOS、Android、Windows 8)上，程式設計師通過Access Enabler客戶端元件與Adobe Primetime身份驗證交互。 此元件有助於與客戶進行所有驗證和授權互動。  Access Enabler在其系統上本地運行。 當用戶訪問程式設計師站點或應用程式並請求內容時，由Adobe托管/維護的Access Enabler元件將靜默載入到後台。

Access Enabler可處理實際的權限工作流，而程式設計師則負責實現用戶介面並與Access Enabler交互的更高級網頁或播放器應用程式。 這些交互是通過非同步的函式和回調系統（由Access Enabler API定義）進行的。

這些是基本權限流，使用Access Enabler API可輕鬆實現：

* 設定請求者（程式設計師）身份
* 檢查/取得針對特定付費電視營運商（「身分提供者」）的使用者驗證
* 檢查/獲取特定資源的用戶授權
* 註銷用戶

Access Enabler還提供以下服務：

* 它驗證來自程式設計師的查詢，包括特定客戶端、其域及其資源/渠道的註冊狀態。
* 它提供建立付費電視營運商清單的資料，使用者可從中選取其提供者。 此清單還根據請求源的程式設計師來驗證和定義。
* 它會啟動付費電視營運商專屬的驗證和授權工作流程。
* 它對每個程式設計師資源/通道的成功授權響應進行快取，以最大限度地減少不必要的請求流量。
* 它可針對每個付費電視營運商專屬的預先定義工作流程進行設定，例如明確的裝置註冊。

根據您的網站或播放器應用程式，Access Enabler可以採用以下形式：

* SWF檔案，Flash Player執行階段可執行
* 由瀏覽器直接執行的JS檔案
* 支援的平台(包括iOS、Android和Windows 8)的本機Access Enabler

#### 無用戶端API {#clientless-api}

無用戶端API方法適用於不支援網頁瀏覽器的「智慧裝置」（遊戲主機、機上盒和智慧電視）（使用MVPD進行驗證時需要）。  在無用戶端方法中，智慧裝置應用程式會透過RESTful網站服務API，直接與Adobe Primetime驗證通訊，以取得除驗證以外的所有功能，驗證會在第二個畫面（瀏覽器）應用程式上執行。 換言之，Access Enabler客戶端庫不被使用。 相反地，智慧裝置應用程式的開發人員會直接使用Adobe Primetime驗證網站服務API來實作權限流程。

### Adobe托管後端伺服器 {#adobe-backend-servers}

由Adobe托管的Adobe Primetime驗證後端伺服器：

* 與需要Adobe Primetime驗證與營運商之間伺服器對伺服器通訊的付費電視提供者布建驗證和授權工作流程。
* 維護程式設計師站點和應用程式的配置。
* 托管可下載的Access Enabler元件檔案。
* 為無客戶端API整合提供RESTful Web服務端點。
* 產生（在某些情況下，還會儲存）驗證和授權Token。

### Token和媒體Token驗證器 {#tokens-media-token-verifier}

Adobe Primetime驗證權限解決方案以產生在成功完成驗證/授權工作流程時所取得的特定資料片段為中心。 這些資料片段稱為代號。 它們的有效期有限，並且安全地儲存在客戶端上與平台相關的位置，或者在無客戶端API解決方案的情況下儲存在Adobe伺服器上。 到期時，必須透過重新啟動驗證和/或授權工作流程來重新核發權杖。

在驗證/授權工作流程期間，Adobe Primetime會發生驗證問題的三種代號類型。 其中兩個是「長期」的，提供了用戶觀看體驗的連續性。 第三種是短期代號，它為業界最佳做法提供支援，以減輕欺詐（例如，欺詐包括流剝離之類的漏洞）。 存留時間(「TTL」)值是根據程式設計人員與付費電視提供者之間的合約而設定，而他們同意最符合相關每個人的價值。

#### （長期）驗證令牌 {#long-lived-auth-token}

一旦客戶使用Adobe Primetime驗證成功登入其付費電視帳戶，就會發生驗證成功。 然後，Adobe Primetime驗證會產生與請求裝置系結的長期驗證(AuthN)代號，並（視付費電視提供者而定）產生匿名識別使用者的全域唯一識別碼(「GUID」)。

* Adobe Primetime驗證會將AuthN權杖安全地儲存在所有使用Adobe Primetime驗證的應用程式皆可使用的位置。 對於Access Enabler整合，令牌安全地儲存在客戶端。  Adobe Primetime驗證會使用AuthN代號，代表使用者提出後續的授權查詢。
* 在任何指定時刻，都只會儲存一個AuthN代號。 每當發出新的AuthN權杖且舊權杖已存在時，新權杖會覆寫現有的儲存值。

#### （長期）授權令牌 {#long-lived-authriz-token}

成功授權後，Adobe Primetime驗證會建立長期授權(「AuthZ」)代號。 此代號無法攜帶，因為它已系結至請求裝置和特定受保護資源（例如頻道、系列或集數）。

* Adobe Primetime驗證會安全地儲存AuthZ代號，以及其他資源的其他授權代號。  同樣，與AuthN令牌一樣，在使用Access Enabler的平台上，令牌儲存在客戶端的本地；在使用無用戶端API的平台上，代號會儲存在Adobe Primetime驗證伺服器上。
* 長存留AuthZ代號的存留時間(TTL)通常會根據付費電視提供者與程式設計師之間的特定協定，在天數到周數的範圍內定義。
* 在任何指定時間，每個資源都只會儲存一個AuthZ代號。 可以儲存多個授權Token，只要這些Token與不同資源相關聯即可。 每當發出新授權權杖，且相同資源已存在舊權杖時，新權杖會覆寫現有的快取值。
* Adobe Primetime驗證使用長期的AuthZ代號來建立用於實際檢視存取的短期媒體代號。

#### 短期媒體代號 {#short-lived-media-token}

一旦Adobe Primetime驗證產生AuthZ代號，就會使用該代號產生由Adobe簽署並加密的單一用途、短期的媒體代號，以避免在交換期間遭到篡改：

* 短期代號的TTL(預設值：5分鐘)，以允許產生令牌的伺服器和驗證令牌的伺服器之間出現時鐘同步問題。
* 短期令牌在提供對受保護資源的訪問之前會暴露在嵌入站點中，因此程式設計師必須使用媒體令牌驗證器來驗證令牌，以便Access Enabler整合，或者在無客戶端API整合的情況下使用令牌驗證器服務。

#### 媒體令牌驗證器 {#media-token-verifier}

程式設計師負責將媒體令牌驗證程式庫整合到其現有的應用程式伺服器中，以便驗證程式能夠在視頻流實際啟動之前執行最終用戶驗證。 媒體令牌驗證程式庫定義：

* 從令牌中檢索資訊的令牌驗證API，例如該令牌是否有效、該令牌的發出時間以及其他相關資料
* 用來驗證代號是否確實來自Adobe的Adobe公開金鑰
* 參考實作，說明如何使用驗證程式API，以及如何使用程式庫中包含的Adobe公開金鑰來驗證其來源

![](assets/high-level-architecture-nflows.png)

*圖2:Access Enabler整合中Adobe Primetime身份驗證生態系統的高級體系結構*

## 與Adobe Primetime驗證整合 {#integrate-auth}

無論您是付費電視提供者或程式設計師，整合Adobe Primetime驗證的程式都需要您參與的程式。 以下將說明這些程式。

### 付費電視提供者程式

付費電視提供商對Adobe Primetime驗證的主要責任是驗證請求用戶確實是有權訪問程式設計師內容的已知訂戶。 從高層面來說，整合新付費電視提供者的Adobe Primetime驗證程式需要下列步驟：

1. 提供者簽署Adobe Primetime驗證保密協定(NDA)。
1. 提供者為Adobe提供其驗證和授權系統的規格。 為了最簡單的整合，建議付費電視營運商具備以SAML為基礎的身分提供者(IdP)以進行驗證，並能透過SOAP存取通訊協定進行通訊以進行授權。
1. 提供者會在其伺服器與Adobe Primetime驗證伺服器之間建立連線。 這包括提供端點和列出IP。
1. 資格預審發佈和量化寬鬆。
1. 生產發行和量化寬鬆。

雖然Adobe Primetime驗證可能會取代程式設計人員現有的整合，但付費電視提供者通常不需要這項功能。 Adobe與提供者的技術團隊合作，設定Adobe Primetime驗證以符合任何現有整合的需求。 假設採用「標準」整合且最低支援需求（檔案和基本電子郵件支援），付費電視提供者可免費整合。 如果提供商需要大量支援或時間表升級，則可能需要支付支援費，或者提供商可能希望與熟悉我們解決方案的第三方（如Synacor）合作。


Adobe Primetime驗證也支援有效處理付費電視提供者業務邏輯，如下所示：

* 對於自包含的業務邏輯，當接收授權請求時，該業務邏輯可被操作員應用，當操作員接收授權請求時，Adobe提供支援業務邏輯執行所需的必要資料。 此資料可包含但不限於提出請求的使用者的唯一裝置ID和裝置的IP位址。
* 對於需要使用者干預和/或由Adobe解決方案具體處理的業務邏輯，Adobe可以維護每個付費電視提供者的一些自訂屬性。 這些運算子專屬的設定/原則包括啟用預先定義的工作流程，這些工作流程可在頂層工作流程的特定點啟動。 如需自訂屬性支援的詳細資訊，請連絡您的Adobe代表。

Adobe還提供欺詐限制服務。 如需詳細資訊，請連絡您的Adobe代表。

### 程式設計人員流程 {#programmer-process}

為了成功整合Adobe Primetime驗證，程式設計人員必須設定其媒體播放器應用程式或網頁，才能在處理核心權限程式時與Adobe Primetime驗證搭配使用：驗證、授權和註銷。


開始與Adobe Primetime驗證整合之前，程式設計人員應：

* 現有的線上視訊平台，包括媒體播放器，作為網站的一部分或作為獨立應用程式
* 內容管理系統
* 一種傳遞機制，其可能包括或不包括第三方內容傳遞網路(CDN)

程式設計人員應該會期望執行一些整合工作，以提供Adobe Primetime驗證的TV Everywhere服務。 這些任務包括：

* 將Adobe Primetime驗證的Access Enabler程式庫整合到您的網頁或媒體播放器中，或使用無用戶端方法對無法上網的「智慧裝置」實作整合
* 伺服器端工作將Adobe Primetime驗證Token驗證器元件整合至您的視訊串流工作流程
* 為進入您的網站或應用程式的存取工作流程建立UI(其中某些元素，例如實際登入程式，由付費電視營運商提供，有些元素可選擇在Adobe Primetime驗證中提供)

本文概述了程式設計人員的流程，Adobe在正式啟動整合時提供了額外的指導。

#### 請求者（程式設計師）設定 {#requester-prog-setup}

##### 向Adobe註冊 {#registering}

首先，程式設計人員必須向Adobe或Adobe授權合作夥伴註冊，並指定他們要與Adobe Primetime驗證搭配使用的網域。 然後，程式設計師接收唯一的請求者ID，該ID被提供給程式設計師與Access Enabler交互的每個會話的Adobe Primetime驗證。

##### 初始Access Enabler整合的設定 {#access-enabler-int-setup}

在任何客戶請求訪問內容之前，程式設計師必須將Adobe Primetime身份驗證客戶端元件(Access Enabler)整合到其現有的媒體播放器應用或網頁中。 有關如何執行此作業，有多種選項：

* 您可以將Flash版本AccessEnabler.swf嵌入到網頁上基於Flash的視頻播放器中，或直接嵌入HTML。 您可以以ActionScript或JavaScript與SWF通訊。 基礎API為ActionScript，但有完整的JavaScript包裝函式程式庫可供使用。
* 對於非Flash裝置，您可以：
   * 使用HTML5/JavaScript版本、AccessEnabler.js，並透過JavaScript API與其通訊，或
   * 使用本機Access Enabler庫，如iOS、Android或Windows 8

##### 初始無用戶端API整合的設定 {#clientless-api-int-setup}

在任何客戶請求訪問內容之前，程式設計師必須使用無客戶端API將RESTful Web服務調用實施到其媒體播放器應用程式中，並設定「第二螢幕」應用程式以處理用戶通過Web登錄到其付費電視提供商的登錄。

#### 處理驗證和授權 {#auth-authr-handling}

當客戶首次向程式設計師請求受保護的資源時，程式設計師向客戶提供要從中選擇的付費電視提供商清單。 當選取提供者時，會將使用者重新導向至該運算子，以進行初始使用者驗證。 一旦驗證成功，Adobe Primetime驗證會與選取的付費電視提供者通訊，以授權存取指定的資源。 以下是這些程式的詳細資訊。

![](assets/providr-selection-ui.png)


*圖3:提供程式選擇UI示例*

>[!NOTE]
>
>* 身為服務提供者（或「SP」）的Adobe Primetime驗證與身分提供者（或「IdP」）的付費電視提供者之間，會以SAML交換的形式發生驗證。
>* 授權使用Adobe Primetime驗證(SP)和付費電視提供者(IdP)之間的後通道（伺服器對伺服器）Web服務交換。



##### 使用Access Enabler的程式設計師通信

Access Enabler與程式設計師網頁或播放器應用之間的雙向通信通道遵循完全非同步模式。 程式設計師通過Access Enabler API公開的方法向Access Enabler發送消息。 Access Enabler通過在Access Enabler庫中註冊的回呼進行響應。

* 如果在本地系統上找不到驗證令牌，則任何授權請求都會自動首先請求驗證。 當驗證成功時，客戶的Token會儲存在本機，因此在指定的一段時間內，他們不需要重新登入。 如果他們已通過Adobe Primetime身份驗證授權解決方案在任何其他上下文（例如，通過付費電視提供商的網站或其他程式設計師）成功地進行身份驗證，則Access Enabler可以訪問本地令牌，並且不需要執行額外的身份驗證。
* 當客戶請求特定資源時，程式設計師通過Access Enabler向付費電視提供商請求授權。 在驗證（或啟動）驗證之後，Access Enabler(通過Adobe Primetime驗證)與付費電視提供商聯繫，以確定客戶是否有權查看資源。 Adobe Primetime驗證會處理與付費電視提供者通訊以取得授權。 程式設計師只需將請求發送到Access Enabler並處理響應（授權是否成功）。 如果授權成功，授權Token會儲存在用戶端系統上，而回呼會接收短時媒體Token。

##### 使用無客戶端API的程式設計師通信 {#progr-comm-clientless-api}

程式設計師應用程式和Adobe Primetime身份驗證之間的通信是通過RESTful Web服務進行的。  所有對Adobe Primetime驗證端點的API呼叫皆具備安全性通訊協定。  無用戶端API檔案中會說明安全性需求。

##### 使用SAML網頁瀏覽器SSO驗證的工作流程範例 {#sample-wf}

1. 檢視器導覽至網站(dummy1.com)並嘗試存取已授權的內容。
1. 視訊頁面/播放器從adobe.com載入Access Enabler ，並在用戶操作提示時，要求獲得所請求內容的授權。
1. Access Enabler運行並驗證請求者和請求。
1. Access Enabler檢查本地儲存中是否有效的授權令牌。 如果找到了有效的授權，則Access Enabler將生成短期介質令牌（請參見步驟14）。
1. 如果未找到對所請求資源的有效授權，但存在有效的驗證令牌，則Access Enabler會向付費電視提供商發起授權請求，該授權請求根據該用戶進行身份驗證。 Adobe伺服器與付費電視提供者提供授權請求/回應交換。
1. 如果未找到有效的驗證令牌，Access Enabler將提示用戶提供其付費電視提供程式。 (選取支援SAML網頁瀏覽器SSO型驗證的提供者，便會觸發SAML型驗證工作流程。 對於非SAML提供者，Adobe會處理類似的自訂工作流程。)
1. Access Enabler將瀏覽器導航到Adobe的SAML SP（服務提供程式）服務，並將其傳遞所有適當的參數。
1. SAML SP會使用IdP中繼資料中指出的SAML網頁瀏覽器設定檔，在使用者的付費電視提供者叫用適當的SAML IdP（身分提供者）。 這樣可有效將使用者導覽至IdP（付費電視提供者）的網站，供使用者驗證。
1. 成功驗證後，系統會將使用者重新導向回Adobe的SAML SP，並在SAML回應中傳遞驗證GUID。
1. Adobe的SAML SP在儲存驗證GUID的伺服器端建立工作階段，並將使用者重新導向回原始的程式設計人員頁面。 （在Access Enabler檢索authN令牌時，將刪除伺服器會話。）
1. Access Enabler從Adobe的伺服器中檢索身份驗證GUID，以將其包含在Token中，該Token具有由Adobe Primetime身份驗證維護的設備ID。 在裝置上FlashDRM時，這會透過Flash AccessAPI(Flash Player的DRM元件)完成，這些API可將GUID系結至裝置ID並傳回驗證Token。 否則，請透過HTTPS的JS API(使用HTML5型儲存)或透過特定原生元件來完成。
1. 驗證令牌由Access Enabler用於向付費電視提供商發出授權請求。 在啟用Flash Access的裝置上，一律會透過Flash AccessAPI提出要求，以便將產生的授權Token系結至裝置。 在非Flash Access裝置上，HTTPS用於從用戶端到伺服器的安全通訊。
1. 成功授權後，Adobe Primetime驗證會建立長期授權(「authZ」)令牌，並將其傳遞至Access Enabler，該Access Enabler將其儲存在本地系統上。
1. Access Enabler使用authZ令牌建立用於實際查看訪問的短時介質令牌。 為了安全起見，這些短期代號必須由其他Adobe Primetime驗證元件（媒體代號驗證器）驗證。

![](assets/authn-authz-entitlmnt-flow.png)


*圖4:驗證和授權Access Enabler工作流*

##### 提供權利用戶介面 {#entitlement-ui}

程式設計師必須建立自己的UI，以便訪問進入其網站或應用程式的工作流。 有些元素（例如實際登入程式）是由付費電視提供者提供，有些元素可選擇在Adobe Primetime驗證中提供。 程式設計師至少會執行以下操作：

* **實現提供程式選擇介面** 這可讓新使用者識別其付費電視提供者，並首次登入。 在開發方面，Access Enabler提供了一個基本的用戶介面，該介面使客戶可以選擇付費電視提供商並啟動登錄過程。 對於生產環境，程式設計師必須實作自己的提供者選取器對話方塊。 有些付費電視提供者會重新導向至自己的網站以進行登入，有些則要求其登入頁面顯示在iframe中。 程式設計人員必須實作可建立此iframe的回呼，以防客戶選擇其中一個提供者。
* **標識受保護的資源。** 受保護的資源是需要授權才能訪問的資源。 在提供這些資源時，程式設計師介面應在查看前指明需要授權。 授權成功後，介面應會顯示資源現已獲授權。
* **建立並維護付費電視提供者清單** 僅控制用戶對您指定的提供程式的訪問。
* **顯示已驗證使用者。** 程式設計師應將客戶的身份驗證狀態作為用於標識受保護資源的任何手段的一部分。 程式設計師可以查詢Access Enabler以確定客戶是否已通過驗證。

#### 支援單次註銷 {#single-logout-support}

在大多數情況下，程式設計師負責通過簡單的API調用處理用戶註銷。 logout()呼叫會指示Primetime驗證，以透過下列方式登出目前使用者：

* 刪除所有AuthN和AuthZ代號
* 清除該用戶的所有身份驗證和授權資訊
* 啟動付費電視提供者專用的工作流程，以清除使用者與提供者的驗證工作階段（例如，如果驗證是使用SAML驗證請求通訊協定完成，則可使用SAML單次登出通訊協定完成登出）。

如果使用者讓電腦閒置足夠的時間讓其代號過期，他們仍可以返回工作階段並成功起始登出。 Adobe Primetime驗證可確保刪除所有代號，並通知付費電視提供者刪除其工作階段。


當從未與Adobe Primetime驗證整合的網站啟動登出時，付費電視提供者可透過瀏覽器重新導向叫用Adobe Primetime驗證單次登出服務。

## 基本權利流程之外 — 其他功能 {#beyond-basics}

基本權限流程包括啟動、驗證、授權和註銷。  隨著Adobe Primetime驗證的成熟和發展，已在基本流程中新增了許多額外功能。  這些包括：

* **使用者中繼資料**  — 根據MVPD與程式設計人員之間的協定，MVPD可以安全地交換元資料，如Zipcode、最大評等、通道ID等。 元資料可啟用各種使用案例，包括家長控制、體育活動的區域凍結期等。
* **臨時自由訪問**  — 讓程式設計師可以臨時免費訪問其受保護的內容（例如，日常寫程式的簡短示例，或大事件的免費演示）。
* **代理MVPD** - MVPD可以管理其與Adobe Primetime驗證的整合，也可以代表一組相關聯的「ProxidMVPD」管理權限程式。

## 安全性 {#security}

本節重點說明Adobe Primetime驗證基礎架構的安全性和完整性。

### 代號安全性 {#token-security}

Adobe Primetime驗證的主要目標之一，是確保系統能夠抵御無賴使用者或內容匯總器對內容權限資料的攻擊。 因此，在工作流中的不同級別保護資料訪問，同時保護具有最高重要性的授權令牌資料的產生和使用。 Adobe Primetime驗證架構的設計目的，是確保Token內容得到安全維護，且Token會保留在核發到的裝置上。

* **長期AuthN和AuthZ代號安全性**  — 所有長期使用的代號皆由Adobe Primetime驗證伺服器以數位方式簽署。 但是，數位簽章不同於平台，因為其使用的裝置ID與其產生、保護和驗證的方式不同。 在所有情況下，用戶端驗證都可確保數位簽章完整無缺，且代號的完整性會保留。 Access Enabler安全地將經過驗證的令牌儲存在運行環境的特定位置。 如果裝置ID驗證失敗，驗證工作階段就會失效、重設代號，並提示使用者重新登入。
* **短期媒體代號安全性**  — 短期媒體令牌在內容訪問前的最後一步生成，由Adobe簽名並加密，以避免在交換期間被篡改。 短期媒體代號也需要額外的Adobe Primetime驗證元件（媒體代號驗證器）執行額外的驗證步驟。 短期代號的TTL會設為5分鐘的預設值，並視需要縮短。 不會快取短期的媒體代號；每次呼叫授權API時，都會從伺服器擷取新代號。

### 平台特定裝置安全性 {#platform-sp-security}

Adobe Primetime驗證使用的安全性措施因平台而異，但都具備強大且最新的功能。

* **啟用Flash的裝置**  — 當裝置上有Flash Player10.1+或AIR 2.5+時，Adobe Primetime驗證會使用Flash PlayerDRM功能進行保護，也稱為Flash Access。 Flash提供了額外的保護級別；以Flash為基礎的代號能有強大的裝置系結保證，這表示在大多數情況下，上線時間可能會更長，使用者不需要經常登入，且使用者體驗一般更流暢。
* **支援HTML5的裝置上的瀏覽器內體驗** — 在包含HTML5瀏覽器功能的非Flash裝置上，Adobe Primetime驗證有其他方法可針對瀏覽器整合提供有限的保護。 不過，由於HTML5的裝置系結不太強大，HTML5平台上代號的存留時間(TTL)通常會較短。
* **對家庭內和家庭外裝置的原生應用程式支援** -Adobe提供每個OS的原生SDK(iOS、Android、Windows 8等) 提供比HTML5解決方案更強的安全性。 這些SDK使用原生API來擷取裝置ID，並安全地將其傳遞至Adobe Primetime驗證伺服器。
* **無用戶端** - Adobe Primetime驗證使用HTTPS通訊協定來進行安全通訊。 此外，來自智慧裝置的所有呼叫都必須進行數位簽署。

## 常見問題集 {#faqs}

**什麼是TV Everywhere?**
被稱為TV Everywhere的行業運動使付費電視用戶能夠訪問他們已經在各種聯網設備上訂購的優質內容，包括個人電腦、平板電腦、智慧手機、遊戲機、機頂盒和「智慧」電視。 此計畫的挑戰在於讓驗證程式盡可能簡單且輕鬆，讓客戶能夠順暢地存取其訂閱內容，而不會受到阻礙並多次登入。


**什麼是Adobe Primetime驗證，它與TV Everywhere有何關係？**
Adobe Primetime驗證可讓TV Everywhere從概念到現實，以簡單且安全的方式順暢地驗證使用者有權存取內容。 Adobe Primetime驗證是托管服務，可根據程式設計人員和付費電視提供者所需的業務規則，進行快速後端整合。 這意味著可以快速向所有交易方營銷、更安全的防欺詐環境，以及更出色的客戶體驗，讓更多的電視內容可供更多平台上的更多用戶使用。


**如何提供/傳遞Adobe Primetime驗證？**
Adobe Primetime驗證是透過軟體即服務(SaaS)模式提供。 這可讓使用者、程式設計人員和付費電視提供者之間進行更安全的通訊，以驗證內容的權限。 服務的核心元件包括用戶端存取啟用碼（或某些裝置的無用戶端API）和托管的Adobe Primetime驗證伺服器。 Access Enabler是一個小檔案，載入到程式設計師的網頁或播放器應用程式中。 它與Adobe Primetime驗證伺服器通訊，而後者又將連線內建在各種付費電視供應商的驗證系統中。 Adobe Primetime驗證也提供無用戶端API方法，以整合某些無法使用Web功能的「智慧裝置」（智慧電視、機上盒、遊戲主機等）。 無用戶端方法提供RESTful Web服務，開發人員可透過這些服務在這些裝置上實作Adobe Primetime驗證權限流程。


**Adobe Primetime驗證與其他TV Everywhere解決方案有何不同？**
Adobe Primetime驗證比替代的TV Everywhere解決方案有明顯的優勢。 當使用者透過網際網路在不同網站間旅行時，與個別提供者的直接整合無法提供單一永久性登入(SSO)的彈性。 Adobe Primetime認證也具有顯著的市場滲透率；一旦程式設計師與Adobe Primetime驗證整合，他們就立即與付費電視運營商連接，這些運營商為美國90%以上的家庭服務。 此外，Adobe Primetime驗證運用Flash執行階段內建的獨特安全性功能（若有），以協助減輕詐騙，同時提供SDK，讓程式設計人員可在無法使用Flash的行動或家庭內裝置的原生應用程式內，內建相同的TV Everywhere功能。 最後，雖然Adobe Primetime驗證是獨立服務，我們也提供選項，以便與其他Adobe產品和服務(包括Primetime和Adobe Analytics)緊密整合，與TV Everywhere內容的傳送、保護和營利相關。

**Adobe Primetime驗證的安全性為何？**
Adobe Primetime驗證架構的第一優先順序是確保只有經過授權的檢視者才能驗證，且能存取優質內容。 Adobe Primetime驗證可將檢視裝置的存取權緊密系結，並有助於限制指定家庭的資料流、工作階段和/或裝置。


**需要Flash Player嗎？**
AdobeFlash Player11.x或更新版本才是最嚴格的設備綁定安全性。 不過，TV Everywhere的Adobe Primetime驗證不受播放器和平台限制，可與任何播放應用程式整合，包括Silverlight和HTML5。 此外，Adobe Primetime驗證也為無法使用Flash Player的裝置(例如iOS、Android和Xbox)提供原生支援。  最後，Adobe Primetime驗證針對無法轉譯網頁（遊戲主控台、智慧電視、機上盒）的裝置，提供無用戶端方法。


**Adobe Primetime驗證支援哪些裝置？**
Adobe Primetime驗證幾乎受到任何具備HTML5網頁套件的裝置所支援，以提供瀏覽器內檢視體驗。 此外，Adobe Primetime驗證仍在針對各種裝置特定平台(包括iOS、Android™和Windows 8)推出原生軟體開發套件(SDK)。 Adobe Primetime驗證部分支援某些非web功能的裝置（智慧電視、機上盒、遊戲主機等） 透過其RESTful網站服務API。

**Adobe Primetime驗證是否支援Tv Everywhere的新興標準？**
Adobe Primetime驗證符合 **CableLabs OLCA（線上內容訪問）** [規格](https://www.cablelabs.com/specifications)，提供從線上來源傳送影片給付費電視客戶的技術需求和架構。 Adobe於2011年6月參與CableLabs整合測試專案，並通過服務提供者實作的測試程式。 Adobe Primetime驗證會根據OLCA規範進行驗證（完整且測試）。 授權元件已完成，但測試驗證正在等待CableLabs測試環境的發佈（ETA 2011年11月）。

Adobe也是 **OATC（開放驗證技術協會）** 並作為該機構的一部分，參與了小組委員會的若干規範起草項目。

**Adobe Primetime驗證如何處理同盟身分管理/單一登入(SSO)?**
Adobe Primetime驗證可讓您使用Adobe Primetime驗證與參與付費電視營運商之間的背向通道（伺服器對伺服器）通訊，為客戶提供單一登入(SSO)驗證和授權。 因此，透過Adobe Primetime驗證，只要付費電視營運商允許持續進行該驗證，訂閱者就不需要在第一次驗證後重新登入。 此限制通常設為30天。 為達此目的，Adobe Primetime驗證為客戶提供驗證Token的通用網域。 與指定付費電視營運商整合的所有參與網站都可使用此驗證狀態資訊。

目前，大部分Adobe Primetime驗證與付費電視營運商的整合都使用SAML通訊協定，這是主要驗證標準之一。 Adobe Primetime驗證在SAML架構中充當代理服務提供者，並將SAML驗證回應保存為Adobe公用網域中的安全Token。 Adobe Primetime驗證符合SAML 2.0。

雖然Adobe Primetime驗證目前通常與SAML SSO解決方案搭配使用，但Adobe Primetime驗證架構會從程式設計師整合中抽取任何協定細節。 因此，可隨時間增加對新通訊協定的支援，例如以OAuth 2.0為基礎或自訂通訊協定。

**一般使用者需花多少錢才能使用TV Everywhere的Adobe Primetime驗證？**
使用Adobe Primetime驗證不需額外付費給使用者。

>[!NOTE]
>
>**後續步驟：** 如需詳細資訊，請連絡您的Adobe代表，或填寫「索取資訊」表單 [此處](https://www.adobe.com/cfusion/mmform/index.cfm?name=adobepass_rfi).
