---
title: Safari瀏覽器的JS SDK限制
description: Safari瀏覽器的JS SDK限制
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Safari瀏覽器的JS SDK限制 {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## Safari 10 {#safari10}

**詳細資料**

* 從Safari 10開始，預設的瀏覽器隱私設定會導致單一登入(SSO)、單一登出(SLO)和被動式驗證功能停止運作。 單一登入(SSO)和被動式驗證即使在多個索引標籤或瀏覽器視窗之間的相同工作階段中也無法運作。

* 這些變更會影響下列AccessEnabler JavaScript SDK版本的Adobe Primetime驗證程式，並對其產生影響：v2（2.x版）、v3（3.x版）、v4（4.x版）。

### 緩解 {#mitigation-safari10}

* 為了緩解這些限制，您可以指示使用者變更Safari 10瀏覽器隱私設定，並使用「**一律允許**「 」選項&#x200B;**Cookie和網站資料**「 」，如下圖所示，從「偏好設定」進入瀏覽器的「隱私權」標籤。

   ![](assets/always-allow-safari10.png)


## Safari 11 {#safari11}

**詳細資料**

>[!IMPORTANT]
>
>若是Safari 11，上述Safari 10部分的所有詳細資料仍適用。

* 從Safari 11開始，瀏覽器會推出 [智慧型追蹤預防](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP)機制，此技術使用試探法來防止跨網站追蹤。 這些試探式作法會影響第三方Cookie的儲存和在網路呼叫上重播的方式，亦即根據啟動的ITP機制，Safari瀏覽器會封鎖用戶端 — 伺服器模型通訊中的第三方Cookie。

* Adobe Primetime驗證服務在驗證程式中使用並依賴Cookie **以便運作**. 在自動進行驗證程式（例如Temp Pass）或使用iFrame或「refressless」功能的實作中，Adobe的Cookie會被視為第三方Cookie，並依預設遭到封鎖。 對於任何其他情況，Safari會使用機器學習演算法，可將所有Adobe的Primetime驗證服務Cookie標幟為追蹤Cookie，因此是ITP封鎖的主旨。  

* 總之，啟用智慧型追蹤預防(ITP)機制後，Safari 11瀏覽器的使用者可能無法在啟用Adobe Primetime驗證的網站上驗證，尤其是當使用者使用多個啟用Adobe主要驗證的網站時。 因此，使用者的驗證體驗可能未預期且未定義，從無法登入到短於預期的驗證期間。

* 這些變更會影響下列AccessEnabler JavaScript SDK版本的Adobe Primetime驗證程式，並對其產生影響：v2（2.x版）、v3（3.x版）。

### 緩解 {#mitigation-safari11}

* 對於AccessEnabler JavaScript SDK v3（3.x版）和AccessEnabler JavaScript SDK v4（4.x版），該庫都包含一種能夠識別因缺少所需Cookie而導致用戶身份驗證被阻止的情況的機制。 在這些情況下，程式庫會觸發特定錯誤回呼 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference)，此資訊會傳回已啟用Adobe Primetime驗證的網站，以作為指示使用者採取可緩解問題的動作的訊號。 為了從此機制中受益，網站必須實作 [錯誤報告](/help/authentication/error-reporting.md) 規範。

* 若為AccessEnabler JavaScript SDK v2（2.x版），程式庫不提供上述機制，因此無法向啟用Adobe Primetime驗證的網站發出指示，指示使用者採取動作以緩解此問題。

* 可緩解上述問題的動作清單 **適用於所有三個版本** AccessEnabler JavaScript SDK的ID。

* 當 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) 實施者的網站收到錯誤回呼，應指示使用者停用智慧型追蹤預防(ITP)並啟用第三方cookie，方法如下：

* 如果是Mac OS X High Sierra及更新版本：取消勾選「**防止跨網站追蹤**&quot;選項&#x200B;**網站追蹤**「 」，如下圖所示，從「偏好設定」進入瀏覽器的「隱私權」標籤。

   ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* 如果是Mac OS X Sierra和以前的：正在檢查「**一律允許**「 」選項&#x200B;**Cookie和網站資料**「 」，如下圖所示，從「偏好設定」進入瀏覽器的「隱私權」標籤。

   ![](assets/always-allow-safari11.png)

## Safari 12 {#safari12}

**詳細資料**

>[!IMPORTANT]
>
>在Safari 12的情況下，上述Safari 10和Safari 11部分的所有詳細資料仍適用。

本節詳細說明的相容性問題 **AccessEnabler JavaScript SDK 4.x版** 在Safari 12上。

>[!NOTE]
>
>請記住，若是AccessEnabler JavaScript SDK 2.x版和AccessEnabler JavaScript SDK 3.x版，兩者都會使用第三方Cookie進行驗證程式，且由於從Safari 11開始的ITP和第三方Cookie原則，使用者的驗證體驗可能未預期且未定義，從無法登入到短於預期的驗證期間。


### Safari 12上AccessEnabler JavaScript SDK v4（4.x版）的認證功能 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **驗證** 即使使用者的瀏覽器已停用第三方cookie，使用者互動的流程仍會一律有效，因為自4.0版開始，AccessEnabler JavaScript SDK不再使用第三方cookie進行驗證程式。

>[!NOTE]
>
>使用者必須與網站互動，才能開啟登入快顯視窗和/或與MVPD登入頁面互動。

* **授權/預檢/使用者中繼資料** 若使用者已通過驗證，則操作可完全運作。

### Safari 12上的AccessEnabler JavaScript SDK v4（4.x版）的已知問題 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO和SLO

   * 由於從Safari 10開始的Safari中實作localStorage的方式，JS SDK無法再透過通用網域iFrame來共用登入狀態。 這表示使用者需要登入使用AccessEnabler JavaScript SDK的每個網站。 登出也不會刪除各個網站的驗證Token，因此使用者必須從每個啟用Adobe Primetime驗證的網站登出。

* 臨時通道

   * 對於臨時傳遞，AccessEnabler JavaScript SDK使用個人化機制，以便將驗證Token鎖定至特定裝置（瀏覽器例項）。 由於Safari 12中的新機制旨在防止追蹤，因此我們正在計算並在個人化機制中使用指紋 **對於具有相同IP位址的所有使用者，都會是相同的**. 我們確實會將用戶端IP視為個人化用途，但即使如此，這也會對共用相同公用IP位址的使用者造成影響。 對於這些使用者，我們會計算相同的個人化id，而臨時傳遞會與其系結。 這表示，一旦這類使用者使用暫時通行證，其他人將無權存取該通行證\! 這尤其會影響企業使用者、教育機構，或任何其他組織，這些組織有多個使用者使用NAT或通用代理來存取網際網路。

>[!NOTE]
>
>此問題只會在實施者因使用者互動而使用Temp Pass時影響使用者，否則Temp Pass驗證可能會受到 **自動流** 下方。

* 自動流

   * 在自動模式中嘗試的驗證流程，若未進行任何使用者互動，使用JS SDK 4.0時，Safari 12中的驗證流程將無法成功。請注意，即將推出的JS SDK 4.1會修正自動化流程的所有問題。

受此問題影響的使用案例：

* 自動TempPass（自由預覽）驗證 — 針對此類流程，SDK會擲回N130錯誤。

* 被動驗證（無訊息失敗） — 系統會要求使用者選取此MVPD並輸入憑證

### 緩解 {#mitigation-safari12}

**SSO和SLO**

目前尚無已知的緩解措施。 Apple確實在Safari 12中導入了「儲存存取API」(`https://webkit.org/blog/8124/introducing-storage-access-api`)，但目前的實作不適用於localStorage，而只適用於cookie。 此外，API需要使用者互動才能使用，而一旦您使用，系統也會以類似下方的權限對話方塊提示使用者。

![](assets/permission-dialog-apple.png)


此時，這些Safari需求/提示不符合我們的UX需求，而且我們的行為也不像其他瀏覽器那樣一致，在其他瀏覽器中，當我們將Token儲存在通用網域localStorage中後，SSO「就會運作」。

**臨時通道**

為了緩解個人化問題，並讓使用者互動，建議您使用 **[促銷臨時通道 ](/help/authentication/promotional-temp-pass.md)** 以互動方式，並提供至少一個關於使用者的額外資訊（例如，電子郵件地址）。

## Safari 13 {#safari13}

**詳細資料**

>[!IMPORTANT]
>
>在Safari 13的情況下，從Safari 10到Safari 12的所有上述詳細資料仍適用。


從Safari 13開始，瀏覽器會對 [智慧型追蹤預防](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP)，讓機制背後的試探式在標示第三方Cookie為追蹤Cookie的程式中更為嚴格，以防止跨網站追蹤。

如前幾節所述，當實作者使用AccessEnabler JavaScript SDK v2（2.x版）和AccessEnabler JavaScript SDK v3（3.x版）時，Adobe Primetime驗證服務會使用並依賴第三方Cookie作為驗證程式的一部分。 與舊版Safari瀏覽器相比，當ITP耗費一段時間以「了解」使用者與相關方(程式設計人員的網站和Adobe)之間的互動時，Safari 13瀏覽器會從第三方Cookie開始封鎖，而第三方Cookie則被視為在用戶端 — 伺服器模型通訊中追蹤Cookie。

總之，Safari 13瀏覽器的使用者很可能無法在啟用Adobe Primetime驗證的網站上啟動新驗證，該網站使用舊版AccessEnabler JavaScript SDK、v2（2.x版）或v3（3.x版）。 這是因為ITP封鎖了所有必要Adobe的Primetime驗證服務Cookie，導致服務無法履行驗證要求。

AccessEnabler JavaScript SDK v4（4.x版）程式庫不使用第三方Cookie進行驗證程式，因此Safari 13變更不會以任何方式影響其操作。

### 緩解 {#mitigation-safari13}

首先，我們強烈建議 **遷移至AccessEnabler JavaScript SDK 4.x版** 以在Safari瀏覽器上擁有穩定且可預測的行為。

其次，對於AccessEnabler JavaScript SDK v3（3.x版），程式庫包含一種機制，可識別因遺失必要Cookie而導致使用者驗證遭到封鎖的情形。 在這些情況下，程式庫會觸發特定錯誤回呼([N130](/help/authentication/error-reporting.md#advanced-error-codes-reference))，此資訊會傳回已啟用Adobe Primetime驗證的網站，以作為指示使用者採取可緩解問題的動作的訊號。 為了從此機制中受益，網站必須實作 [錯誤報告](/help/authentication/error-reporting.md) 規範。

若為AccessEnabler JavaScript SDK v2（2.x版），程式庫不提供上述機制，因此無法向啟用Adobe Primetime驗證的網站發出指示，指示使用者採取動作以緩解此問題。

當 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) 實施者的網站收到錯誤回呼，應指示使用者停用智慧型追蹤預防(ITP)並啟用第三方cookie，方法如下：

* 如果是Mac OS X High Sierra及更新版本：取消勾選「**防止跨網站追蹤**&quot;選項&#x200B;**網站追蹤**「 」，如下圖所示，從「偏好設定」進入瀏覽器的「隱私權」標籤。

   ![](assets/prvnt-cross-site-tr-safari13.png)

* 如果是Mac OS X Sierra和以前的：正在檢查t</span>he」**一律允許**「 」選項&#x200B;**Cookie和網站資料**「 」，如下圖所示，從「偏好設定」進入瀏覽器的「隱私權」標籤。

   ![](assets/always-allow-safari13.png)

