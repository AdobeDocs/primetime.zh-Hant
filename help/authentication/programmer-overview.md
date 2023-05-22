---
title: 程式設計師概述
description: 程式設計師概述
exl-id: 64a12e49-0ecb-4b81-977d-60c10925bb59
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---

# 程式設計師概述 {#programmers-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#introduction}

本概述適用於計畫將Adobe® Pass整合到其網站或應用程式的內容提供商（程式設計師）。 有關包括Kickstart和整合指南在內的其他文檔，請參閱下面的相關資訊。

現在，您的觀眾可以隨時隨地上網，並直接向您（程式設計師）請求訪問受保護的內容。 他們可能想看一次性活動，或者他們可能正在為你正在播出的整個電視劇爭取收視權。

但是，在您允許訪問受保護的內容之前，您必須確定客戶是否有權查看該內容。 他們是否訂購了多通道視頻寫程式分發伺服器(MVPD)? 如果是，該訂閱是否包括您的程式？

對於程式設計師來說，確定查看者的權利並不總是簡單。 MVPD擁有其客戶的標識資料和訪問權限。  添加以下事實：試圖訪問受保護內容的查看者訂閱了各種MVPD ，每個MVPD都有不同的系統，而且很容易看到，確定查看者對受保護內容的權利可能很快變得複雜，而且在技術上具有挑戰性：

![](assets/user-ent-by-progr.png)

*圖：由程式設計師直接確定的用戶權利*

Adobe Primetime對TV Everywhere的身份驗證可安全地協調程式設計師和MVPD之間的這些權利事務。 Adobe Primetime認證使程式設計師能夠輕鬆、快速、安全地向有效客戶提供受保護的內容：

![](assets/user-ent-mediatedby-authn.png)

*圖：用戶權利由Adobe Primetime身份驗證介紹*

Adobe Primetime身份驗證在與參與的MVPD的交換中充當代理，因此您可以向查看者提供一致的跨站點介面。 Adobe Primetime身份驗證還允許您為查看者提供單點登錄(SSO)身份驗證和授權。 跟蹤所有參與服務的驗證和授權，以便訂戶無需在其自己的系統上第一次驗證後再次登錄。

* **驗證**  — 使用MVPD確認給定用戶是已知客戶的過程。
* **授權**  — 使用MVPD確認已驗證用戶對指定資源有效訂閱的過程。

### Adobe Primetime驗證工作原理 {#HowItWorks}

程式設計師的內容查看應用程式使用Access Enabler客戶端元件或無客戶端API的REST風格的Web服務（用於智慧電視、遊戲控制台、機頂盒等非Web功能設備）與Adobe Primetime驗證交互。 Access Enabler在用戶的系統上運行，方便了所有權利工作流。  當客戶訪問您的站點並請求受保護的內容時，Access Enabler元件將從其托管站點Adobe下載。  Adobe Primetime認證伺服器托管無客戶端解決方案中使用的REST風格的Web服務。

Adobe Primetime身份驗證處理實際的權利工作流，同時提供您用於：

* 設定您的身份。 (程式設計師是Adobe Primetime身份驗證權限流中的「請求者」。)
* 使用特定MVPD驗證用戶。  (MVPD是Adobe Primetime身份驗證權利流中的「身份提供程式」或「IdP」。)
* 為特定資源授權具有MVPD的用戶。
* 註銷用戶。

程式設計師負責執行以下操作的高級網頁或播放器應用程式：

* 實現用戶介面
* 與Access Enabler或無客戶端API Web服務交互

Adobe Primetime身份驗證的目標是為程式設計師和MVPD建立一種簡單、模組化的方式來處理權利驗證。

## 瞭解令牌 {#understanding-tokens}

Adobe Primetime認證權利解決方案的核心是在成功完成認證和授權工作流後建立的特定資料片段的生成。 這些資料被稱為令牌。 令牌的壽命有限；當令牌過期時，需要通過重新啟動身份驗證和授權工作流來重新頒發令牌。

有關令牌的詳細資訊，請參閱以下各節：

* [令牌類型](#token-types)
* [令牌儲存](#token-storage)
* [令牌安全性](#token-security)
* [令牌共用](#token-sharing)

### 令牌類型 {#token-types}

在驗證和授權工作流期間發出三種類型的令牌。 AuthN和AuthZ令牌是「長期」的，提供了用戶的查看體驗的連續性。 Media Token是一個短命的令牌，它為業界最佳做法提供支援，以防止通過流翻錄欺詐。 程式設計師根據與MVPD達成的協定為每種類型的令牌指定生存時間(TTL)值。 程式設計師們決定一個TTL值，它最適合您的企業和客戶。

* **AuthN令牌** （「長壽」）:成功驗證後，Adobe Primetime驗證將建立與請求設備和全局唯一標識符(GUID)相關聯的AuthN令牌。
   * Adobe Primetime身份驗證將AuthN令牌發送到Access Enabler ,Access Enabler將其安全地快取在客戶端系統上。  當AuthN令牌存在且未到期時，它可用於所有使用Adobe Primetime身份驗證的應用程式。 Access Enabler使用AuthN令牌進行授權流。
   * 在任何給定時刻，都只快取一個AuthN令牌。 只要發出新的AuthN令牌且舊令牌已存在，Adobe Primetime身份驗證就會覆蓋快取令牌。
* **AuthZ令牌** （「長壽」）:成功授權後，Adobe Primetime認證將建立與請求設備和特定受保護資源關聯的AuthZ令牌。  受保護資源由唯一資源ID標識。
   * Adobe Primetime身份驗證將AuthZ令牌發送到Access Enabler ,Access Enabler將其安全地快取到本地系統。 然後，Access Enabler使用AuthZ令牌建立用於實際查看訪問的短時間媒體令牌。
   * 在任何給定時間，每個資源只快取一個AuthZ令牌。 Adobe Primetime身份驗證可以快取多個AuthZ令牌，只要它們與不同的資源相關聯。 只要發出新的AuthZ令牌且同一資源已存在舊令牌，Adobe Primetime身份驗證就會覆蓋快取令牌。
* **媒體令牌** （「短命」）:Access Enabler使用AuthZ令牌生成短時(預設值：7分鐘)媒體令牌。 這是成功的播放請求被認為發生的點。
   * 在提供對受保護資源的訪問之前，媒體伺服器必須使用Adobe Primetime驗證元件（媒體令牌驗證器）來驗證媒體令牌。
   * 由於媒體令牌未綁定到設備，因此其壽命會顯著縮短(預設值：7分鐘)。
   * 短時間媒體令牌被限制為一次性使用，並且從不快取。 每次調用授權API時，都從Adobe Primetime驗證伺服器檢索該API。

### 令牌儲存 {#token-storage}

Access Enabler將長期令牌（AuthN和AuthZ）儲存在其環境特定的位置：

* **Flash10.1** （或更高）:長壽命的令牌儲存為本地共用對象。
* **HTML5**:長壽命的令牌被安全地保存在HTML5瀏覽器的本地儲存中。
* **iOS**:長壽命令牌被儲存在持久貼上板上，在該貼上板上，其他Adobe Primetime認證客戶端應用程式可訪問它們。
* **安卓**:長壽命的令牌儲存在共用資料庫檔案中，在該檔案中，其他Adobe Primetime認證客戶端應用程式可訪問它們。
* **無客戶端API設備**:令牌儲存在黃金時段驗證伺服器上。

### 令牌安全性 {#token-security}

Adobe Primetime認證伺服器使用設備ID（從設備的硬體特性派生）對所有長壽命令牌進行數字簽名。 數字簽名的生成、保護和驗證方式因環境而異：

* **Flash10.1** （或更高） — 設備ID依賴於設備憑據，即從Adobe個性化伺服器頒發的唯一證書。 此安全性相當於FAXS DRM技術。 此伺服器端驗證將令牌中的唯一設備ID與設備憑據進行比較(從Flash Player安全地通信到Adobe Primetime驗證)。 設備憑據還標識FAXS客戶端版本和向其頒發的Flash Player(或AIR)版本。 設備綁定比HTML5更強，因此令牌的生存時間(TTL)通常比Flash更長。
* **HTML5**  — 該設備在客戶端是個性化的。 它使用通過JavaScript提供的特性來生成偽設備ID，該偽設備ID包括瀏覽器和作業系統版本、IP地址和瀏覽器cookie GUID（全局唯一標識符）。 將此令牌設備ID與設備的當前偽設備ID進行比較。 由於IP地址在正常使用期間可能會發生更改，因此，即使在同一會話中，Adobe Primetime身份驗證也會將HTML5個令牌儲存在兩個位置：localStorage和sessionStorage。 如果IP更改，並且sessionStorage令牌仍然有效，則會維護會話。 對於HTML5，設備綁定不是那麼強，因此令牌的TTL通常比Flash短。
* **本地客戶端** (iOS和Android) — 長期令牌保存本機設備ID個性化資訊，因此綁定到請求設備。 驗證和授權請求通過HTTPS發送，設備ID資訊在發送到後端伺服器之前由Access Enabler庫進行數字簽名。 在伺服器端，根據其關聯的數字簽名來驗證設備ID資訊。
* **無客戶端API客戶端**  — 無客戶端API解決方案具有其一組安全協定，這些協定涉及對所有API調用進行數字簽名。 在權利流期間生成的令牌被安全地儲存在Adobe Primetime認證伺服器上。

Adobe Primetime驗證會驗證每個長期令牌，以確保訪問內容的設備與發出令牌的設備相同。 對於所有令牌，客戶端驗證確保數字簽名完整，並保留令牌的完整性。 當設備ID驗證失敗時，驗證會話無效，並且提示用戶再次登錄，這將重置令牌。

### 令牌共用 {#token-sharing}

不同平台上的應用程式不共用令牌。 原因有多，包括：

* 如所述 [令牌儲存](#token-storage)，儲存令牌的方法因平台而異(例如，用於Flash的本地共用對象、用於JavaScript的WebStorage)。
* 不同平台之間令牌安全程度不同。 例如，Flash令牌使用FAXS強烈綁定到設備。 純JavaScript環境中的令牌的DRM支援級別與Flash中的令牌級別不同。  與Flash應用程式共用JS令牌會增加利用更安全環境的不安全令牌的可能性。

## 程式設計師整合生命週期 {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*圖：將身份驗證與程式設計師網站和應用程式整合*


## 邏輯流 {#logical-flows}

### 權利流程圖 {#chart}

以下流程圖顯示確認權利的整個過程(使用Adobe Primetime驗證Access Enabler客戶端元件):

![](assets/ent-flowchart.png)

*圖：確認權利的過程*

### 驗證步驟 {#authn-steps}

以下步驟提供了Adobe Primetime身份驗證流的示例。  這是權利流程的一部分，程式設計師在該流程中確定用戶是否是MVPD的有效客戶。  在此方案中，用戶是MVPD的有效訂閱者。  用戶正試圖使用程式設計師的Flash應用程式查看受保護的內容：

1. 用戶瀏覽到程式設計師的網頁，該網頁將程式設計師的Flash應用程式和Adobe Primetime驗證訪問啟用程式元件載入到用戶的電腦上。 Flash應用程式使用Access Enabler將程式設計師的標識與Adobe Primetime身份驗證一起設定，而Adobe Primetime身份驗證將Access Enabler與該程式設計師（「請求者」）的配置和狀態資料一起設定為質。 Access Enabler必須先從伺服器接收此資料，然後才能執行任何其他API調用。 技術說明：程式設計師使用Access Enabler設定其標識 `setRequestor()` 方法；有關詳細資訊，請參閱 [程式設計師整合指南](/help/authentication/programmer-integration-guide-overview.md)。
1. 當用戶嘗試查看程式設計師的受保護內容時，程式設計師的應用程式向用戶提供MVPD清單，用戶從該清單中選擇提供商。
1. 用戶被重定向到Adobe Primetime認證伺服器，其中加密 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 建立用戶選定MVPD的請求。 此請求以代表程式設計師的身份驗證請求發送到MVPD。 根據MVPD的系統，用戶的瀏覽器隨後會被重定向到MVPD的站點以登錄，或者在程式設計師的應用中建立登錄iFrame。
1. 在兩種情況下（重定向或iFrame）,MVPD都會接受請求並顯示其登錄頁。
1. 用戶使用MVPD登錄，MVPD將驗證用戶作為付費客戶的狀態，然後MVPD將建立自己的HTTP會話。
1. 驗證用戶後，MVPD將建立響應（SAML和加密）,MVPD將響應發回Adobe Primetime驗證。
1. Adobe Primetime驗證接收MVPD響應，發現有一個Adobe Primetime驗證HTTP會話開啟，驗證來自MVPD的SAML響應，並重定向回程式設計師站點。
1. 重新載入程式設計師站點，重新載入Access Enabler，程式設計師再次調用setRequestor()。  對setRequestor()的第二次調用是必需的，因為當前配置已更改 — 現在存在一個標誌，它通知Access Enabler AuthN令牌正等待在伺服器上生成。
1. Access Enabler發現存在掛起的身份驗證，並從Adobe Primetime身份驗證伺服器請求令牌。 通過調用Flash Player的DRM功能從伺服器檢索令牌。
1. AuthN令牌儲存在程式設計師Flash PlayerLSO快取中；驗證現在已完成，會話在Adobe Primetime驗證伺服器上被銷毀。

### 授權步驟 {#authz-steps}

繼續執行以下步驟 [驗證步驟](#authn-steps):

1. 當用戶嘗試訪問程式設計師的受保護內容時，程式設計師的應用程式首先檢查用戶的本地電腦或設備上的AuthN令牌。  如果那個令牌不在，那麼 [驗證步驟](#authn-steps) 上。  如果AuthN令牌存在，則授權流將繼續由程式設計師的應用程式啟動對Access Enabler的調用，請求獲取用戶對特定受保護內容項的查看權限。
1. 受保護內容的特定項由「資源標識符」表示。  這可以是簡單的字串或更複雜的結構，但無論如何，資源標識符的性質是預先在程式設計師和MVPD之間商定的。  程式設計師的應用程式將資源標識符傳遞給Access Enabler。  Access Enabler會檢查用戶的本地電腦或設備上的AuthZ令牌。  如果AuthZ令牌不在，Access Enabler會將請求傳遞給後端Adobe Primetime身份驗證伺服器。
1. Adobe Primetime認證伺服器使用標準化協定與MVPD授權端點通信。  如果MVPD的響應指示用戶有權查看受保護的內容，則Adobe Primetime身份驗證伺服器會建立一個AuthZ令牌並將其傳回Access Enabler,Access Enabler將AuthZ令牌儲存在用戶的電腦上。
1. 使用儲存在用戶機器或設備上的AuthZ令牌，程式設計師的應用程式調用Access Enabler從Adobe Primetime認證伺服器獲取媒體令牌，並將該令牌提供給程式設計師應用程式。
1. 最後，程式設計師的應用程式使用媒體令牌驗證器元件來確認正確的用戶正在查看正確的內容，並且在媒體令牌就位後，允許用戶查看受保護的內容。


## 註冊和初始化 {#reg-and-init}

使用Adobe Primetime認證的第一步是向Adobe或Adobe Primetime認證授權的合作夥伴註冊。

註冊時，將提供與Adobe Primetime身份驗證通信的域清單。 例如，Turner廣播系統域包括tbs.com和tnt.tv作為Adobe Primetime認證註冊域。 這些內容站點中的每個站點都被授予對Adobe Primetime身份驗證的訪問權限，並被分配其自己的請求者ID（例如，「TBS」和「TNT」）。 如果您決定添加其他站點，則必須通知Adobe其他域名，以便將它們放在允許的域清單上並給予其他請求者ID。

>[!WARNING]
>
>在測試整合時，請確保test伺服器位於要在生產中使用的註冊域上。 來自非白名單域的請求(甚至是test請求)將被忽略。 例如，如果您請求在生產中使用domain.com，請確保在domain.com、test.domain.com和staging.domain.com下部署test整合。
>
>即使在URL中列出了白名單，也會忽略包含用戶名和/或密碼的請求。 示例： `//username@registered-domain/`

請求者ID在與Adobe Primetime驗證的Access Enabler客戶端元件的所有通信中唯一標識程式設計師客戶端。 與程式設計師關聯的所有Adobe Primetime驗證靜態資料都被鎖定到此ID。

>[!TIP]
>
>除了請求者ID之外，在註冊時還會收到Access Enabler客戶端元件和媒體令牌驗證器的功能URL。

## 整合步驟 {#integration-steps}

>[!TIP]
>
>如果將Adobe的Open Source Media Framework(「OSMF」)用於媒體播放器開發，則使用Adobe Primetime身份驗證的最快方式是整合OSMF插件 *（不建議使用）* 你玩家的密碼。
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [請求者設定](#requestor)
1. [處理身份驗證和授權](#authn-authz)
1. [支援單次註銷](#ssl)

### 1。請求者設定 {#requestor}

#### 1a 註冊到Adobe

第一步是向Adobe或Adobe Primetime身份驗證授權合作夥伴註冊。  註冊時，系統會向您發出一個或多個全局唯一標識符(GUID)。 您發出的每個GUID都與允許訪問Adobe Primetime身份驗證的域關聯。 為請求域傳遞GUID（稱為請求者ID），以註冊您與Access Enabler交互的每個會話的標識。 有關詳細資訊，請參閱 [註冊和初始化](#reg-and-init) 的上界。

#### 1b 初始Access Enabler整合

下一步是將Access Enabler整合到您現有的媒體播放器應用程式或網頁中：

* 你可以嵌入Flash版， `AccessEnabler.swf`，在基於Flash的視頻播放器中，或者您可以直接將其嵌入到網頁的HTML中。 您可以在ActionScript或JavaScript中與Access EnablerSWF通信。 基本API是ActionScript，但如果您希望使用JavaScript，則可以在您的頁面中包含一個完整的包裝庫。
* 對於非Flash環境，您可以：
   * 使用HTML5/JavaScript版本AccessEnabler.js，並通過JavaScript API與其通信
   * 使用AIR本地擴展進行Adobe Primetime身份驗證，將本地代碼與內置ActionScript類組合
   * 使用Access Enabler庫(iOS或Android)的一個本機客戶端版本

### 2.處理身份驗證和授權 {#authn-authz}

#### 2a 與Access Enabler通信

Access Enabler與您的網頁或播放器應用之間的通信是非同步的。 您的應用程式調用Access Enabler方法，Access Enabler通過在Access Enabler庫中註冊的回叫進行響應。

* 當您的應用程式發出授權請求時，如果本地系統上尚未有有效的AuthN令牌，Access Enabler將自動啟動身份驗證請求。 驗證成功後，用戶的AuthN令牌將本地儲存，因此不需要再次登錄。 如果他們已在任何其他上下文（例如，通過MVPD網站或使用其他程式設計師）中通過Adobe Primetime身份驗證成功進行身份驗證，則Access Enabler有權訪問本地AuthN令牌，而且不需要附加身份驗證。
* 當用戶嘗試訪問受保護的內容時，您會向Access Enabler發送授權請求。 驗證（或啟動）身份驗證後，Access Enabler將聯繫MVPD(通過Adobe Primetime身份驗證伺服器)，以確定客戶是否有權查看受保護的內容。 您的應用程式只需將請求發送到Access Enabler，然後處理響應（授權成功或失敗）。 如果授權成功，則AuthZ令牌將儲存在客戶端系統上。  最後，您的應用程式將收到一個短時間的媒體令牌，用於您自己的授權過程。

>[!NOTE]
>
>* 身份驗證作為SAML交換，在作為服務提供方(SP)的Adobe Primetime身份驗證和作為身份提供方(IdP)的MVPD之間發生。
>
>* 授權使用Adobe Primetime身份驗證(SP)和MVPD(IdP)之間的後通道（伺服器到伺服器）Web服務交換。



#### 2b 提供權利用戶介面 {#entitlement-ui}

您提供您自己的UI，以便用戶訪問您的內容。 某些元素（如實際登錄過程）由MVPD提供，而某些元素可選地作為Adobe Primetime驗證的一部分可用。 至少，執行以下操作：

* **實現MVPD選擇介面，該介面允許新用戶標識其MVPD並首次登錄**。 在開發中，Access Enabler提供了一個基本的用戶介面，該介面為客戶提供了MVPD選項並啟動登錄過程。 對於生產，必須實現自己的MVPD選擇器對話框。 某些MVPD重定向到其自己的站點進行登錄，有些則要求其登錄頁面在iFrame中顯示。 必須實現建立此iFrame的回調，以處理用戶的MVPD在iFrame中顯示其登錄頁的情況。
* **識別受保護的內容**。 受保護的內容需要授權才能訪問。 您的介面應指示哪些內容受保護，哪些內容已經授權。  授權狀態通常用「已解鎖」和「已鎖定」表徵圖來表示。
* **顯示已驗證用戶**。 您應將用戶的身份驗證狀態作為標識受保護內容的任何手段的一部分。 您可以查詢Access Enabler以確定客戶是否已經過身份驗證。

#### 2c 整合媒體令牌驗證器 {#int-media-token-ver}

必須將Adobe Primetime身份驗證媒體令牌驗證器元件整合到媒體伺服器中。  這樣，您的現有令牌驗證程式就可以識別通過成功授權從Adobe Primetime身份驗證提供的短時間媒體令牌。 媒體令牌驗證器將媒體令牌驗證為提供用戶對受保護內容的訪問之前的最後一個安全步驟。 在註冊Adobe時，您將收到從中下載媒體令牌驗證器的位置。

### 3.支援單次註銷 {#ssl}

在大多數情況下，您的媒體播放器負責通過簡單的Access Enabler API處理用戶註銷。 調用logout()時，Access Enabler將執行以下操作：

* 註銷當前用戶
* 清除已註銷用戶的所有身份驗證和授權資訊
* 從用戶的本地系統中刪除所有AuthN和AuthZ令牌

如果用戶讓其電腦空閒足夠長，其令牌將過期，則用戶仍可返回會話並成功啟動註銷。 Adobe Primetime驗證確保刪除所有令牌，並通知MVPD刪除其會話。

當從未與Adobe Primetime驗證整合的站點啟動註銷時，MVPD可以通過瀏覽器重定向調用Adobe Primetime驗證單次註銷服務。

## 瞭解用戶ID {#user-ids}

從概念上講，啟動權利流的每個用戶都與單個唯一用戶ID相關聯。  但是，在權利流程中，一個用戶ID可以以不同的方式顯示，具體取決於您從哪個API獲取ID。

短媒體令牌中的sessionGUID是UserID的安全形式，可通過sendTrackingData()調用獲得。   在所有當前整合中，這是跨時間和設備的用戶的持久GUID，但GUID的源以MVPD的SAML響應中的UserID開始。   但是，某些MVPD可能會在將來改變主意，並開始發送臨時GUID。  如果程式設計師希望確保AuthN響應中的MVPD源UserID是持久的，則他們應在與MVPD的協定中安排。

以下是用戶ID在Adobe Primetime驗證API中的不同表示方式：

* `sendTrackingData()` GUID屬性 — 這是MVPD UserID的Adobe散列版本。  已散列，因此此用戶ID無法從MVPD跟蹤回源。   此ID是唯一的，通常是持久的，但無法與MVPD共用，以將特定使用行為與MVPD在其一側的使用行為進行比較。   它沒有數字簽名，因此不是防欺詐的不可欺騙，但是它足夠用於分析。  在AuthN/AuthZ流中Adobe Primetime身份驗證生成的所有事件上，都提供了此形式的用戶ID。
* 短媒體令牌 `sessionGUID` 屬性 — 與UserID相同，通過 `sendTrackingData()`但是，這個是數字簽名，以保護其完整性。  這樣，該值就足夠用於同時使用的欺詐跟蹤。 在使用我們的驗證程式庫之後，它將在伺服器端進行處理，並且可以在將視頻流發佈到客戶端之前分析欺詐模式。  任何這些任務都由程式設計師負責。
* `getMetadata() userID `屬性 — 此屬性允許Adobe向程式設計師公開實際源MVPD UserID。 它將使用程式設計師提供的證書中的公鑰進行加密，這樣客戶端就不會將其公開。 這為程式設計師提供了MVPD中的實際用戶ID，因此它可用於直接與MVPD進行帳戶連結或欺詐調查。

**最後**

* MVPD用戶ID通常是永久唯一ID, **從MVPD生成，並在成功驗證時傳遞給Adobe**。 它通常在所有網路中都是一致的，但有些例外。
* MVPD用戶ID不包含PII，並且它不是帳號。 不需要以加密形式公開它，因為我們已通過所有未發送PII的MVPD驗證。


用戶ID的使用方式取決於用例：

* 如果您需要它進行跟蹤/分析，最實際的地方就是從 `sendTrackingData()`。
* 如果在伺服器端需要它來獲取流釋放、欺詐或操作資料，可以從媒體令牌驗證器獲取。
* 如果您需要它來進行帳戶連結和更深入的欺詐活動，請與Adobe聯繫人聯繫以瞭解其可用性。

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->
