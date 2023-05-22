---
title: 關於Adobe Primetime認證和TV Everywhere
description: 關於Adobe Primetime認證和TV Everywhere
exl-id: 5edeaccb-f9fa-4395-83b4-706c518d5a03
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '6288'
ht-degree: 0%

---

# 關於Adobe Primetime認證和TV Everywhere {#about-auth-tve}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 關於TV Everywhere {#about-tve}

如今的電視觀眾可以隨時隨地上網，他們期望自己能夠隨身訪問付費電視內容。 此外，觀眾正在使用越來越多的可使用網際網路的設備查看內容，包括：

* 筆記型電腦
* 片劑
* 智慧手機
* 網站
* 聯合應用
* 遊戲機
* 機頂盒
* 智慧電視

TV Everywhere是一項行業運動，它支援付費電視用戶在家中和家中外，通過多種設備訪問他們已經付費的內容。 儘管大部分電視觀看仍在常規線性電視上進行，但消費增長是時移內容、線上視頻和替代螢幕。 結果，如今的視頻發行市場處於混亂狀態，而TV Everywhere已經成為協調程式設計師、付費電視提供商和付費電視用戶利益的解決方案。


TV Everywhere的技術目標是使付費TV客戶能夠訪問其所有設備和平台上已經訂閱的內容。


TV Everywhere的業務目標是：

* **保留現有客戶關係並啟用新關係**
* 使程式設計師和內容所有者能夠接觸到最廣的受眾，並從高級內容中獲取更多價值
* 通過直接與觀眾進行線上互動擴展品牌

## TV無處不在的挑戰 {#tve-challenges}

隨著&quot;無處不在&quot;電視的機遇，也帶來挑戰。 這些問題的核心是權利。 在查看者訪問訂閱內容之前，必須有人確定他們是否有權訪問訂閱內容。

用戶是否與付費電視提供商訂閱？ 如果是，該訂閱是否包括正在請求的內容？ 對程式設計師和內容所有者來說，權利要求特別難以直接確定，因為付費電視運營商擁有客戶的識別資料以及客戶的訪問權限。


除權利外，還有許多相關的技術和整合挑戰，包括：

* 制定和實施綜合多設備策略
* 協調程式設計師與付費電視提供商之間的各種關係
* 防止欺詐性訪問或濫用服務條款
* 為跨網站和應用的用戶提供一致且無挫折感的身份驗證體驗
* 保持快速上市時間，以跟上關聯交易
* 管理與多個整合相關的成本

這些挑戰使程式設計師與多個付費電視提供商的身份驗證系統之間執行和維護複雜、直接的整合非常耗費資源，需要時間和技術上的成熟。


解決方案？ **Adobe®黃金時段身份驗證**。

## Adobe Primetime身份驗證簡介 {#authentication-intro}

通過Adobe Primetime認證，程式設計師和付費電視提供商只需進行簡單的整合，使用Adobe Primetime認證API即可訪問整個生態系統，包括：

* 特納廣播(TBS,TNT,CNN)，福克斯廣播網和Hulu等程式設計師

* 美國所有頂級付費電視提供商，佔美國所有付費電視家庭的90%以上

此外，Adobe Primetime認證還提供了使用戶認證和授權變得簡單和安全的框架。

![](assets/programmers-connect-authn.png)

*圖1:只是一些通過Adobe Primetime驗證連接的程式設計師和付費電視提供商……*

Adobe Pass公司安全地協調程式設計師和付費電視提供商之間的權利交易，方便觀眾訪問訂閱內容。 換句話說……

**Adobe Primetime身份驗證使適當的客戶能夠輕鬆快速地訪問適當的內容。**

**Adobe Primetime是誰的認證？**

* **程式設計師** 希望輕鬆與付費電視提供商（又稱「MVPD」或「多渠道視頻節目分發商」）整合，以獲得最佳收入的受眾。 使用Adobe Primetime認證，程式設計師可以對所有主要提供商的查看者進行認證，而不依賴於客戶端平台。

* **付費電視提供商/MVPD** 通過方便線上訪問訂閱內容，他們尋求與多個程式設計師輕鬆連接，並提高客戶滿意度。

* **付費電視客戶** 希望輕鬆訪問他們已經訂閱的內容，無論他們在哪裡，都無需額外付費。 單點登錄提供了跨Web或跨移動應用的安全查看器身份驗證，而不需要客戶端下載或重複登錄，也不需要良好的用戶體驗。

對於 **程式設計師**,Adobe Primetime驗證提供：

* 與頂級付費電視提供商輕鬆整合和即時連接，而無需進行多個直接整合
* 通過支援盡可能廣泛的內容受眾來優化訂閱（許可）和廣告收入
* 安全身份驗證，只向授權用戶/設備授予對高級內容的訪問權限
* 一個開放且靈活的框架，它不受玩家和DRM平台的限制；可在多種平台上進行播放，包括iOS、Android、Windows 8、遊戲控制台、機頂盒等。
* 與任何DRM技術(如AdobeFlash Access®或Play Ready®)的相容性。
* 支援單一登錄(SSO)身份驗證和授權，這樣訂戶就無需在其自己的系統上第一次身份驗證後再次登錄。


對於 **付費電視提供商/MVPD**,Adobe Primetime驗證提供：

* 輕鬆與內容所有者整合，通過單一整合與多個程式設計師提供即時連接
* 通過支援平滑的品牌體驗來增強客戶參與能力，因為他們可以跨多個平台和設備查看內容
* 安全身份驗證，確保僅授權授權用戶/設備訪問高級內容，並（可選）限制可以連接每個家庭帳戶的設備和併發流的數量。


對於 **付費電視客戶**,Adobe Primetime驗證提供：

* **到處看電視！**

本文對Adobe Primetime認證技術進行了介紹。  雖然下面的大部分內容都側重於程式設計師整合，但也有適用於付費電視提供商的一般資訊和特定資訊。 本文檔還突出了Adobe Primetime認證作為TV Everywhere解決方案的安全性和完整性。 有關本白皮書之外的詳細資訊，請與您的Adobe代表聯繫或填寫「資訊請求」表單 [這裡](https://www.adobe.com/)。

## 建築砌塊 {#arch-building-blocks}

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/import-pc7mz3dfnv/check.gif) 下面將討論身份驗證和授權的中央權利事務。 身份驗證是向付費電視提供商確認給定用戶是已知客戶的過程。 授權是付費電視提供商確認經過認證的用戶對給定資源具有有效訂閱的過程。
Adobe Primetime驗證由以下基本元件組成：

* 客戶端元件（下列元件之一）:

   * Access Enabler — 特定於平台的庫；提供易於使用的API和代碼示例，用於實現權利流
   * 無客戶端API - REST風格的Web服務；為沒有網頁呈現功能的平台（如遊戲機、機頂盒等）提供權利流終結點

* Adobe承載的後端伺服器
* 媒體令牌驗證器
* 安全的中央交換介質（令牌）

在基本級別，Adobe Primetime身份驗證由三個元件(訪問啟用程式、承載Adobe的後端伺服器和媒體令牌驗證程式)和一個中心交換項（令牌）組成。

### 客戶端元件 {#client-components}

* 訪問啟用碼
* 無客戶端API

#### 訪問啟用碼 {#access-enabler}

在完全支援的平台(包括Web、iOS、Android、Windows 8)上，程式設計師通過Access Enabler客戶端元件與Adobe Primetime身份驗證進行交互。 此元件方便了與客戶進行的所有身份驗證和授權交互。  Access Enabler在其系統上本地運行。 當用戶訪問程式設計師站點或應用程式並請求內容時，Adobe托管/維護的Access Enabler元件將靜默載入到後台。

Access Enabler可處理實際的權利工作流，而程式設計師則負責實現用戶介面並與Access Enabler交互的更高級網頁或播放器應用程式。 這些交互是通過由Access Enabler API定義的非同步函式和回調系統進行的。

這些是基本權利流，使用Access Enabler API可輕鬆實現：

* 設定請求者（程式設計師）標識
* 針對特定付費電視運營商（「身份提供商」）檢查/獲取用戶身份驗證
* 檢查/獲取特定資源的用戶授權
* 註銷用戶

Access Enabler還提供以下服務：

* 它驗證來自程式設計師的查詢，包括特定客戶端、其域及其資源/渠道的註冊狀態。
* 它提供建立付費電視運營商清單的資料，用戶從中選擇其提供商。 此清單還針對請求發源的程式設計師進行驗證和定義。
* 它啟動付費電視運營商特定的身份驗證和授權工作流。
* 它快取每個程式設計師資源/通道的成功授權響應，以最大限度地減少不必要的請求流量。
* 它可以針對特定於每個付費電視操作員的預定義工作流進行配置，如顯式設備註冊。

根據您的網站或播放器應用程式，Access Enabler可以採用以下形式：

* SWF運行時可以執行的Flash Player檔案
* 瀏覽器直接執行的JS檔案
* 支援的平台(包括iOS、Android和Windows 8)的本機Access Enabler

#### 無客戶端API {#clientless-api}

無客戶端API方法適用於不支援Web瀏覽器（使用MVPD進行身份驗證時需要）的「智慧設備」（遊戲控制台、機頂盒和智慧電視）。  在無客戶端方法中，智慧設備應用通過REST風格的Web服務API直接與Adobe Primetime驗證通信，以用於除身份驗證之外的所有內容，該身份驗證在第二螢幕（瀏覽器）應用上執行。 換句話說，不使用Access Enabler客戶端庫。 相反，智慧設備應用的開發者直接使用Adobe Primetime認證Web服務API來實現權利流。

### Adobe承載的後端伺服器 {#adobe-backend-servers}

Adobe Primetime身份驗證後端伺服器，由Adobe承載：

* 向付費電視提供商提供身份驗證和授權工作流，這些提供商需要Adobe Primetime身份驗證和運營商之間的伺服器到伺服器通信。
* 維護程式設計師站點和應用程式的配置。
* 承載可下載的Access Enabler元件檔案。
* 為無客戶端API整合提供REST風格的Web服務終結點。
* 生成（在某些情況下，儲存）身份驗證和授權令牌。

### 令牌和媒體令牌驗證器 {#tokens-media-token-verifier}

Adobe Primetime認證授權解決方案的核心是在成功完成認證/授權工作流後獲得的特定資料片段的生成。 這些資料被稱為令牌。 它們的使用壽命有限，並且安全地儲存在客戶端上與平台相關的位置，或者在無客戶端API解決方案的情況下儲存在Adobe伺服器上。 到期後，必須通過重新啟動驗證和/或授權工作流來重新發佈令牌。

在驗證/授權工作流中，有三種類型的令牌會導致Adobe Primetime驗證問題。 二是&quot;長壽&quot;，提供用戶觀看體驗的連續性。 第三種是短命的令牌，它為減輕欺詐的行業最佳做法提供了支援（例如，欺詐包括流翻錄等利用漏洞）。 生存時間(「TTL」)值是根據程式設計師和付費電視提供商之間的協定設定的，這些提供商同意一個最能為所有相關人員服務的價值。

#### （長期）身份驗證令牌 {#long-lived-auth-token}

一旦客戶使用Adobe Primetime身份驗證成功登錄其付費電視帳戶，驗證就會成功。 Adobe Primetime認證隨後產生與請求設備相關聯的長壽命認證(AuthN)令牌，並（取決於付費電視提供商）匿名標識用戶的全局唯一標識符(「GUID」)。

* Adobe Primetime驗證將AuthN令牌安全地儲存在所有使用Adobe Primetime驗證的應用程式都可使用的位置。 對於Access Enabler整合，令牌在客戶端安全地儲存。  Adobe Primetime身份驗證使用AuthN令牌代表用戶進行後續授權查詢。
* 在任何給定時刻都只儲存一個AuthN令牌。 只要發出新的AuthN令牌且舊令牌已存在，新令牌將覆蓋現有儲存值。

#### （長期）授權令牌 {#long-lived-authriz-token}

成功授權後，Adobe Primetime身份驗證將建立長期授權(「AuthZ」)令牌。 此令牌不可移植，因為它與請求設備和特定受保護資源（例如，頻道、系列或插集）相關聯。

* Adobe Primetime身份驗證將AuthZ令牌與其他資源的其他授權令牌一起安全地儲存。  同樣，與AuthN令牌一樣，在使用Access Enabler的平台上，令牌儲存在客戶端本地；在使用無客戶端API的平台上，令牌儲存在Adobe Primetime驗證伺服器上。
* 長壽命AuthZ令牌的生存時間(TTL)通常在天到周的範圍內定義，具體取決於付費電視提供商與程式設計師之間的特定協定。
* 在任何給定時間，每個資源只儲存一個AuthZ令牌。 可以儲存多個授權令牌，只要它們與不同的資源相關聯。 只要頒發了新的授權令牌，並且同一資源的舊授權令牌已存在，新令牌就會覆蓋現有的快取值。
* Adobe Primetime身份驗證使用長壽命的AuthZ令牌建立短壽命的媒體令牌，這些令牌用於實際查看訪問。

#### 短期媒體令牌 {#short-lived-media-token}

一旦Adobe Primetime驗證生成AuthZ令牌，它就使用該令牌生成由Adobe簽名並加密的一次性短效媒體令牌，以避免在交換期間篡改：

* 短期令牌的TTL(預設值：5分鐘)設定為允許在生成令牌的伺服器和驗證令牌的伺服器之間出現時鐘同步問題。
* 在提供對受保護資源的訪問之前，短命令會暴露在嵌入站點中，因此程式設計師必須使用Access Enabler整合的媒體令牌驗證器或無客戶端API整合的令牌驗證器服務來驗證令牌。

#### 媒體令牌驗證器 {#media-token-verifier}

程式設計師負責將媒體令牌驗證程式庫整合到其現有應用程式伺服器中，以便驗證程式可以在視頻流實際啟動之前執行最終用戶驗證。 媒體令牌驗證器庫定義：

* 從令牌中檢索資訊的令牌驗證API，例如，該令牌是否有效、該令牌的發出時間以及其它相關資料
* 用於驗證令牌是否確實來自Adobe的Adobe公鑰
* 一個參考實現，顯示如何使用Verifier API以及如何使用庫中包含的Adobe公鑰驗證其源

![](assets/high-level-architecture-nflows.png)

*圖2:Access Enabler整合中Adobe Primetime身份驗證生態系統的高級體系結構*

## 與Adobe Primetime身份驗證整合 {#integrate-auth}

無論您是付費電視提供商還是程式設計師，與Adobe Primetime身份驗證整合的過程都需要您的積極參與。 下面介紹了這些過程中的每一個。

### 付費電視提供商流程

付費電視提供商對Adobe Primetime認證的主要責任是驗證請求用戶確實是有權訪問程式設計師內容的已知用戶。 從高層面講，Adobe Primetime認證過程需要執行以下步驟來與新付費電視提供商整合：

1. 提供商簽署Adobe Primetime身份驗證保密協定(NDA)。
1. 提供商為Adobe提供其驗證和授權系統的規範。 為了實現最簡單的整合，建議付費電視運營商具有基於SAML的身份提供程式(IdP)進行身份驗證，並能夠通過SOAP訪問協定進行通信以進行授權。
1. 提供程式在其伺服器和Adobe Primetime身份驗證伺服器之間建立連接。 這包括提供端點和列出IP。
1. 資格預審釋放和量化寬鬆。
1. 生產發放和量化寬鬆。

雖然Adobe Primetime身份驗證可能會取代程式設計師的現有整合，但付費電視提供商通常不需要這種整合。 Adobe與提供商的技術團隊合作，配置Adobe Primetime身份驗證以滿足任何現有整合的需要。 對付費電視提供商來說，整合是免費的，假定整合是「標準」的，支援要求是最低的（文檔和基本電子郵件支援）。 如果提供商需要大量支援或升級時間表，可能需要支付支援費用，或者提供商可能希望與熟悉我們解決方案的第三方合作。


Adobe Primetime認證還支援對付費電視提供商業務邏輯的有效處理，如下所示：

* 對於自包含且當接收到授權請求時可由運營商應用的業務邏輯，Adobe在運營商接收到授權請求時提供支援業務邏輯強制所需的必要資料。 此資料可以包括但不限於發出請求的用戶的唯一設備ID和設備的IP地址。
* 對於需要用戶干預和/或由Adobe解決方案進行特定處理的業務邏輯，Adobe可以為每個付費電視提供商維護一些自定義屬性。 這些特定於操作員的配置/策略包括啟用預定義的工作流，這些工作流可以在頂級工作流的特定點啟動。 有關自定義屬性支援的詳細資訊，請與Adobe代表聯繫。

Adobe還提供欺詐限制服務。 請與Adobe代表聯繫以瞭解詳細資訊。

### 程式設計師流程 {#programmer-process}

要成功整合Adobe Primetime認證，程式設計師必須設定其媒體播放器應用程式或網頁，以便在處理核心權利流程時與Adobe Primetime認證協作：驗證、授權和註銷。


在開始與Adobe Primetime身份驗證整合之前，程式設計師應具備：

* 現有線上視頻平台，包括媒體播放器，作為網站的一部分或作為獨立應用
* 內容管理系統
* 一種遞送機制，其可以包括或不包括第三方內容遞送網路(CDN)

程式設計師應該期望執行一些整合任務，作為通過Adobe Primetime驗證提供TV Everywhere服務的一部分。 這些任務包括：

* 將Adobe Primetime驗證的Access Enabler庫整合到您的網頁或媒體播放器中，或使用無客戶端方法實現不支援Web的「智慧設備」的整合
* 將Adobe Primetime身份驗證令牌驗證器元件整合到視頻流工作流中的伺服器端工作
* 為網站或應用中的訪問工作流建立UI(其中一些元素，如實際登錄過程，由付費電視操作員提供，某些元素可選地作為Adobe Primetime身份驗證的一部分提供)

本白皮書概述了程式設計師流程，Adobe在正式啟動整合時提供了附加指導。

#### 申請人（程式設計師）設定 {#requester-prog-setup}

##### 註冊Adobe {#registering}

作為第一步，程式設計師必須向Adobe或Adobe授權的合作夥伴註冊，並指定他們希望與Adobe Primetime身份驗證一起使用的域。 程式設計師接著接收唯一的請求者ID，該請求者ID被提供給程式設計師與Access Enabler交互的每個會話的Adobe Primetime驗證。

##### 初始Access Enabler整合的設定 {#access-enabler-int-setup}

在任何要求訪問內容的客戶之前，程式設計師必須將Adobe Primetime驗證客戶端元件 — Access Enabler — 整合到他們現有的媒體播放器應用或網頁中。 有關如何執行此操作有多種選擇：

* 您可以將Flash版本AccessEnabler.swf嵌入到基於Flash的視頻播放器的網頁上，或直接嵌入HTML。 可以在ActionScript或JavaScript中與SWF通信。 基API是ActionScript，但是有一個完整的JavaScript包裝庫。
* 對於非Flash設備，您可以：
   * 使用HTML5/JavaScript版本AccessEnabler.js，並通過JavaScript API與其通信，或
   * 使用本機Access Enabler庫，如用於iOS、Android或Windows 8

##### 初始無客戶端API整合的設定 {#clientless-api-int-setup}

在任何要求訪問內容的客戶之前，程式設計師必須將使用無客戶端API的REST風格的Web服務調用實現到其媒體播放器應用中，並設定「第二螢幕」應用程式以處理用戶通過Web登錄到其付費電視提供商的登錄。

#### 處理身份驗證和授權 {#auth-authr-handling}

當客戶首次向程式設計師請求受保護資源時，程式設計師向客戶提供要從中選擇的付費電視提供商清單。 當選擇提供程式時，用戶被重定向到該操作員以進行初始用戶驗證。 一旦驗證成功，Adobe Primetime驗證將與選定付費電視提供商通信以授權對指定資源的訪問。 以下是這些流程的詳細資訊。

![](assets/providr-selection-ui.png)


*圖3:提供程式選擇UI示例*

>[!NOTE]
>
>* 身份驗證是作為服務提供商（或「SP」）的Adobe Primetime身份驗證和作為身份提供商（或「IdP」）的付費電視提供商之間的SAML交換。
>* 授權使用Adobe Primetime身份驗證(SP)和付費電視提供商(IdP)之間的後通道（伺服器到伺服器）Web服務交換。



##### 使用Access Enabler的程式設計師通信

Access Enabler與程式設計師網頁或播放器應用程式之間的雙向通信通道遵循完全非同步模式。 程式設計師通過Access Enabler API公開的方法向Access Enabler發送消息。 Access Enabler通過在Access Enabler庫中註冊的回調進行響應。

* 如果在本地系統上找不到驗證令牌，則任何授權請求都會自動先請求驗證。 驗證成功後，客戶的令牌將儲存在本地，這樣他們就不需要在給定時間段內再次登錄。 如果他們在任何其他上下文（例如通過付費電視提供商的網站或其他程式設計師）中通過Adobe Primetime身份驗證權限解決方案成功地進行了身份驗證，則Access Enabler有權訪問本地令牌，並且不需要執行額外的身份驗證。
* 當客戶請求特定資源時，程式設計師通過Access Enabler向付費電視提供商請求授權。 驗證（或啟動）身份驗證後，Access Enabler會聯繫付費電視提供商(通過Adobe Primetime身份驗證)，以確定客戶是否有權查看該資源。 Adobe Primetime認證處理與付費電視提供商通信以獲得授權。 程式設計師只需將請求發送到Access Enabler並處理響應（授權成功或失敗）。 如果授權成功，則授權令牌被儲存在客戶機系統上，並且回調接收短壽命的媒體令牌。

##### 使用無客戶端API的程式設計師通信 {#progr-comm-clientless-api}

程式設計師應用程式與Adobe Primetime身份驗證之間的通信是通過REST風格的Web服務進行的。  對Adobe Primetime驗證端點的所有API調用都有安全協定。  安全要求在無客戶端API文檔中介紹。

##### 基於SAML Web瀏覽器SSO的工作流驗證示例 {#sample-wf}

1. 查看器導航到站點(dummy1.com)並嘗試訪問有權訪問的內容。
1. 視頻頁面/播放器從adobe.com載入Access Enabler，當用戶操作提示時，請求對請求的內容進行授權。
1. Access Enabler運行並驗證請求者和請求。
1. Access Enabler檢查本地儲存中的有效授權令牌。 如果找到有效的授權，則Access Enabler將生成短時間的介質令牌（請參見步驟14）。
1. 如果找不到對請求的資源的有效授權但存在有效的驗證令牌，則Access Enabler會向付費電視提供商發起授權請求，該用戶將根據該請求進行身份驗證。 Adobe伺服器提供與付費電視提供商的授權請求/響應交換。
1. 如果找不到有效的驗證令牌，Access Enabler將提示用戶輸入付費電視提供商。 (選擇支援基於SAML的Web瀏覽器SSO的驗證的提供程式會觸發基於SAML的驗證工作流。 對於非SAML提供程式，Adobe處理類似的自定義工作流。)
1. Access Enabler將瀏覽器導航到Adobe的SAML SP（服務提供程式）服務，並將其傳遞所有適當的參數。
1. SAML SP使用IdP元資料中指示的SAML Web瀏覽器配置檔案，在用戶的付費電視提供程式處調用相應的SAML IdP（身份提供程式）。 這有效地將用戶導航到用戶驗證的IdP（付費電視提供商）站點。
1. 成功驗證後，用戶將重定向回Adobe的SAML SP，並在SAML響應中向其傳遞身份驗證GUID。
1. Adobe的SAML SP在儲存身份驗證GUID的伺服器端建立會話，並將用戶重定向回原始的「程式設計師」頁。 （在Access Enabler檢索authN令牌時刪除伺服器會話。）
1. Access Enabler從Adobe的伺服器中檢索身份驗證GUID，以將其包含在令牌中，該令牌具有由Adobe Primetime身份驗證維護的設備ID。 當FlashDRM在設備上時，通過Flash AccessAPI(Flash Player的DRM元件)完成，這些API允許將GUID綁定到設備ID並返回驗證令牌。 否則，通過HTTPS上的JS API使用基於HTML5的儲存或通過特定的本機元件完成此操作。
1. Access Enabler使用身份驗證令牌向付費電視提供商發出授權請求。 在啟用Flash Access的設備上，請求總是通過Flash AccessAPI發出，以便將產生的授權令牌綁定到設備。 在非Flash Access設備上，HTTPS用於從客戶端到伺服器的安全通信。
1. 成功授權後，Adobe Primetime身份驗證將建立一個長期授權(「authZ」)令牌，並將其傳遞給Access Enabler，後者將其儲存在本地系統上。
1. Access Enabler使用authZ令牌建立用於實際查看訪問的短時間媒體令牌。 為了安全起見，這些短命令必須由另一個Adobe Primetime驗證元件（媒體令牌驗證器）驗證。

![](assets/authn-authz-entitlmnt-flow.png)


*圖4:驗證和授權Access Enabler工作流*

##### 提供權利用戶介面 {#entitlement-ui}

程式設計師必須建立自己的UI，以便將訪問工作流導入其網站或應用。 某些元素（如實際登錄過程）由付費電視提供商提供，而某些元素可選地作為Adobe Primetime驗證的一部分可用。 程式設計師至少執行以下操作：

* **實現提供程式選擇介面** 允許新用戶識別其付費電視提供商並首次登錄。 在開發過程中，Access Enabler提供了一個基本的用戶介面，該介面為客戶提供了付費電視提供商的選擇並啟動登錄過程。 對於生產環境，程式設計師必須實現其自己的提供程式選擇器對話框。 有些付費電視提供商重定向到自己的站點進行登錄，有些提供商要求在iframe中顯示其登錄頁。 程式設計師必須實現建立此iframe的回調，以防客戶選擇其中一個提供程式。
* **標識受保護的資源。** 受保護資源是指需要授權訪問的資源。 在提供這些資源時，程式設計師介面應在查看前指示需要授權。 如果授權成功，則介面應顯示該資源現在已被授權。
* **建立並維護付費電視提供商清單** 以僅控制用戶對指定的提供程式的訪問。
* **顯示已驗證用戶。** 程式設計師應指出客戶的身份驗證狀態，作為用於標識受保護資源的任何手段的一部分。 程式設計師可以查詢Access Enabler以確定客戶是否已經過身份驗證。

#### 支援單次註銷 {#single-logout-support}

在大多數情況下，程式設計師負責通過簡單的API調用處理用戶註銷。 logout()調用通過以下方式指示Mogine身份驗證註銷當前用戶：

* 刪除所有AuthN和AuthZ令牌
* 清除該用戶的所有身份驗證和授權資訊
* 啟動付費電視提供方特定的工作流以清除用戶與提供方的驗證會話（例如，如果驗證是使用SAML驗證請求協定完成的，則可以使用SAML單次註銷協定完成註銷。）

如果用戶讓其電腦空閒足夠時間，使其令牌過期，則他們仍然可以返回其會話並成功啟動註銷。 Adobe Primetime驗證確保刪除所有令牌，並通知付費電視提供商刪除其會話。


當從未與Adobe Primetime認證整合的站點啟動註銷時，付費電視提供商可以通過瀏覽器重定向調用Adobe Primetime認證單次註銷服務。

## 除基本權利流之外 — 附加功能 {#beyond-basics}

基本權利流是啟動、驗證、授權和註銷。  隨著Adobe Primetime認證的成熟和發展，已經和正在向基本流中添加一些附加功能。  這些包括：

* **用戶元資料**  — 根據MVPD與程式設計師之間的協定，MVPD可以安全地交換元資料，如Zipcode、最大評級、通道ID等。 元資料支援各種使用案例，包括家長控制、體育賽事的區域凍結期等。
* **臨時可用訪問**  — 允許程式設計師臨時免費訪問其受保護的內容（例如，日常節目的簡短示例或大型事件的免費演示）。
* **代理MVPD** - MVPD可以管理其與Adobe Primetime身份驗證的整合，還可以代表一組關聯的「ProxiedMVPD」管理權利進程。

## 安全 {#security}

本節重點介紹Adobe Primetime身份驗證基礎架構的安全性和完整性。

### 令牌安全性 {#token-security}

Adobe Primetime身份驗證的主要目標之一是確保系統能夠抵御流氓用戶或內容聚合器對內容權利資料的攻擊。 因此，在工作流中的不同級別上保護資料存取，同時保護具有最高重要性的授權令牌資料的生成和使用。 Adobe Primetime認證體系結構設計為確保令牌內容被安全維護並且令牌保留在其所發佈的設備上。

* **長壽命AuthN和AuthZ令牌安全**  — 所有長壽命的令牌都由Adobe Primetime驗證伺服器進行數字簽名。 但是，數字簽名不同於平台，因為它使用的設備ID在生成、保護和驗證方式上不同。 在所有情況下，客戶端驗證都可確保數字簽名完好無損，並保留令牌的完整性。 Access Enabler將驗證的令牌安全地儲存在運行該令牌的環境的特定位置。 如果設備ID驗證失敗，驗證會話將失效，令牌被重置，並提示用戶再次登錄。
* **短期媒體令牌安全**  — 在內容訪問之前的最後一步中生成的短壽命媒體令牌通過Adobe簽名並加密，以避免在交換期間篡改。 短壽命的媒體令牌還需要通過額外的Adobe Primetime驗證元件（媒體令牌驗證器）執行額外的驗證步驟。 短壽命令牌的TTL設定為預設值5分鐘，如果需要，可縮短。 短時間的媒體令牌從不快取；每次調用授權API時，都會從伺服器中檢索新令牌。

### 特定於平台的設備安全 {#platform-sp-security}

Adobe Primetime身份驗證使用的安全措施因平台而異，但都是強健的、最先進的。

* **啟用Flash的設備**  — 當Flash Player10.1+或AIR2.5+位於設備上時，Adobe Primetime驗證使用Flash PlayerDRM功能進行保護，也稱為Flash Access。 Flash提供額外的保護；對基於Flash的令牌的設備綁定的強大保證意味著在大多數情況下，生存時間可以更長，用戶不必經常登錄，並且用戶體驗通常更流暢。
* **在支援HTML5的設備上的瀏覽器內體驗** — 在包括HTML5瀏覽器功能的非Flash設備上，Adobe Primetime身份驗證為基於瀏覽器的整合提供了有限保護的替代方法。 但是，由於HTML5的設備綁定不是那麼強，因此HTML5平台上的令牌的生存時間(TTL)通常會更短。
* **本地應用程式支援家庭內和家庭外設備** -Adobe提供每作業系統的本機SDK(iOS、Android、Windows 8等) 為HTML5解決方案提供增強的安全性。 這些SDK使用本機API檢索設備ID並將其安全地傳遞給Adobe Primetime驗證伺服器。
* **無客戶端** -Adobe Primetime身份驗證使用HTTPS協定進行安全通信。 此外，來自智慧設備的所有呼叫都必須進行數字簽名。

## 常見問題 {#faqs}

**哪裡有電視？**
行業運動TV Everywhere使付費電視客戶能夠在各種網際網路連接設備上訪問他們已經訂閱的優質內容，這些設備包括個人電腦、平板電腦、智慧手機、遊戲機、機頂盒和「智慧」電視。 此計畫的挑戰是使身份驗證過程盡可能簡單和輕鬆，使客戶能夠順利訪問其訂閱內容，而不會遇到阻礙和多次登錄。


**什麼是Adobe Primetime認證，它與TV Everywhere有何關係？**
Adobe Primetime驗證通過以簡單和安全的方式平穩地驗證用戶對內容的權利，將TV Everywhere從概念轉變為現實。 Adobe Primetime認證是一種托管服務，它允許基於程式設計師和付費電視提供商要求的業務規則進行快速後端整合。 這意味著需要快速向所有方面營銷，提供更安全的環境來防止欺詐，並提供卓越的客戶體驗，讓更多的電視內容能夠跨更多平台提供給更多人。


**如何提供/提供Adobe Primetime身份驗證？**
Adobe Primetime認證通過軟體即服務(SaaS)模式提供。 這使最終用戶、程式設計師和付費電視提供商之間能夠進行更安全的通信，以驗證對內容的權利。 服務的核心元件包括客戶端訪問啟用程式（或某些設備的無客戶端API）和托管的Adobe Primetime認證伺服器。 Access Enabler是一個小檔案，載入到程式設計師的網頁或播放器應用程式中。 它與Adobe Primetime認證伺服器通信，而後者又將連接內置到各種付費電視提供商的認證系統中。 Adobe Primetime認證還為某些不能使用Web的「智慧設備」（智慧電視、機頂盒、遊戲機等）提供了無客戶端API整合方法。 無客戶端方法提供REST風格的Web服務，開發人員可以利用這些服務在這些設備上實施Adobe Primetime身份驗證權限流。


**Adobe Primetime身份驗證與其他TV Everywhere解決方案有何不同？**
Adobe Primetime認證比其他TV Everywhere解決方案有明顯的優勢。 與單個提供商的直接整合在用戶跨Internet從站點到站點旅行時，不提供單一、持續登錄(SSO)的靈活性。 Adobe Primetime認證也具有顯著的市場滲透性；一旦程式設計師與Adobe Primetime認證整合，他們就立即與付費電視運營商連接，為美國90%以上的家庭服務。 此外，Adobe Primetime身份驗證還利用內置於Flash運行時（可用時）的獨特安全功能來幫助減輕欺詐，同時還提供SDK，以便程式設計師可以將相同的TV Everywhere功能內置於本地應用中，用於不提供Flash的移動或家庭內設備。 最後，雖然Adobe Primetime認證可作為獨立服務提供，但我們也提供了與其他Adobe產品和服務(包括黃金時段和Adobe Analytics)緊密整合的選項，這些產品和服務與TV Everywhere內容的交付、保護和貨幣化有關。

**Adobe Primetime身份驗證有多安全？**
Adobe Primetime認證架構的首要任務是確保只有經過授權的查看者才能被認證並被授予對高級內容的訪問權限。 Adobe Primetime認證將訪問查看設備緊密綁定，並有助於限制給定家庭的流、會話和/或設備。


**是否需要Flash Player?**
AdobeFlash Player11.x或更高版本是最嚴格的設備綁定安全所必需的。 但是，TV Everywhere的Adobe Primetime身份驗證與播放器和平台無關，與任何播放應用程式(包括Silverlight和HTML5)整合。 此外，Adobe Primetime身份驗證還為無法Flash Player的設備(如iOS、Android和Xbox)提供本機支援。  最後，Adobe Primetime認證為無法呈現網頁（遊戲機、智慧電視、機頂盒）的設備提供了無客戶端方法。


**Adobe Primetime驗證支援哪些設備？**
Adobe Primetime認證幾乎受任何帶有HTML5 Web工具包的設備支援，以便在瀏覽器內查看體驗。 此外，Adobe Primetime身份驗證正在繼續為各種特定於設備的平台(包括iOS、Android™和Windows 8)推出本機軟體開發包(SDK)。 Adobe Primetime身份驗證部分支援某些非Web功能設備（智慧電視、機頂盒、遊戲機等） 通過其REST風格的Web服務API。

**Adobe Primetime認證是否支援新興的TV Everywhere標準？**
Adobe Primetime驗證符合 **CableLabs OLCA（線上內容訪問）** [規格](https://www.cablelabs.com/specifications)它提供了從線上源向付費電視客戶交付視頻的技術要求和體系結構。 Adobe於2011年6月參與了CableLabs的聯合互動測試項目，並通過了服務提供商實施的測試流程。 Adobe Primetime驗證是根據OLCA規範進行驗證的（完整和測試）。 授權元件已完成，但測試驗證正在等待CableLabs測試環境（ETA 2011年11月）的發佈。

Adobe也是 **OATC（開放認證技術聯盟）** 作為該機構的一部分，參加了幾個小組委員會的規範起草項目。

**Adobe Primetime身份驗證如何處理聯合身份管理/單點登錄(SSO)?**
Adobe Primetime認證允許您通過Adobe Primetime認證和參與付費電視運營商之間的後台（伺服器到伺服器）通信，為客戶提供單點登錄(SSO)認證和授權。 因此，使用Adobe Primetime驗證，用戶無需在第一次驗證後重新登錄，只要付費電視運營商允許該驗證持續。 通常，此限制設定為30天。 為此，Adobe Primetime認證為我們的客戶提供了一個通用的認證令牌域。 此驗證狀態資訊可用於與給定付費電視運營商整合的所有參與站點。

目前，Adobe Primetime與付費電視運營商的大多數身份驗證整合都使用SAML協定，這是主要的身份驗證標準之一。 Adobe Primetime驗證在SAML體系結構中充當代理服務提供程式，並將SAML驗證響應作為安全令牌在Adobe公共域中保留。 Adobe Primetime驗證符合SAML 2.0。

雖然Adobe Primetime身份驗證通常在此時與SAML SSO解決方案一起使用，但Adobe Primetime身份驗證體系結構從程式設計師整合中抽取任何協定細節。 因此，可以隨著時間的推移增加對新協定的支援，例如基於OAuth 2.0或自定義協定的協定。

**TV Everywhere的Adobe Primetime身份驗證對最終用戶來說要花多少錢？**
最終用戶使用Adobe Primetime身份驗證不需額外付費。

>[!NOTE]
>
>**後續步驟：** 有關詳細資訊，請與Adobe代表聯繫或填寫「資訊請求」表單 [這裡](https://www.adobe.com/cfusion/mmform/index.cfm?name=adobepass_rfi)。
