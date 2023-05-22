---
title: Safari瀏覽器的JS SDK限制
description: Safari瀏覽器的JS SDK限制
exl-id: 5e5c3b36-ee09-49e0-b5b7-83b24854d69d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Safari瀏覽器的JS SDK限制 {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## 野生動物園10 {#safari10}

**詳細資訊**

* 從Safari 10開始，預設的瀏覽器隱私設定將導致單一登錄(SSO)、單一註銷(SLO)和被動身份驗證功能停止工作。 單一登錄(SSO)和被動身份驗證即使在多個頁籤或瀏覽器窗口之間的同一會話中也無法正常工作。

* 這些更改會影響並影響以下版本的AccessEnabler JavaScript SDK的Adobe Primetime身份驗證進程：v2（2.x版）、 v3（3.x版）、 v4（4.x版）。

### 緩解 {#mitigation-safari10}

* 為了減輕這些限制，您可以指示用戶更改Safari 10瀏覽器隱私設定，並使用「 」**始終允許**&quot;選項&#x200B;**Cookie和網站資料**»在瀏覽器的「隱私」頁籤的「首選項」中輸入，如下圖所示。

   ![](assets/always-allow-safari10.png)


## 野生動物園11 {#safari11}

**詳細資訊**

>[!IMPORTANT]
>
>在Safari 11的情況下，Safari 10節中的所有上述詳細資訊仍然適用。

* 從Safari 11開始，瀏覽器介紹 [智慧跟蹤防範](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP)機制，一種使用啟發式來防止跨站點跟蹤的技術。 這些啟發式方法會影響在網路呼叫中儲存和重播第三方Cookie的方式，這意味著根據ITP機制激活，Safari瀏覽器將阻止客戶端 — 伺服器模型通信中的第三方Cookie。

* Adobe Primetime身份驗證服務使用並依賴Cookie作為身份驗證過程的一部分 **為了發揮作用**。 在自動進行身份驗證過程（如臨時通過）或在使用iFrames或「refressless」功能的實現中，Adobe的cookie被視為第三方cookie，預設情況下被阻止。 對於其他任何情況，Safari都使用機器學習算法，該算法可能會將所有Adobe的黃金時段身份驗證服務Cookie標籤為跟蹤Cookie，因此受ITP阻塞的制約。  

* 總之，在激活智慧跟蹤預防(ITP)機制後，Safari 11瀏覽器的用戶可能無法在啟用Adobe Primetime驗證的網站上進行驗證，特別是當用戶使用啟用多個Adobe優先驗證的網站時。 因此，用戶的身份驗證體驗可能是意外和未定義的，從無法登錄到比預期的身份驗證持續時間短。

* 這些更改會影響並影響以下版本的AccessEnabler JavaScript SDK的Adobe Primetime身份驗證進程：v2（2.x版）、 v3（3.x版）。

### 緩解 {#mitigation-safari11}

* 對於AccessEnabler JavaScript SDK v3（3.x版）和AccessEnabler JavaScript SDK v4（4.x版），庫都包含一種機制，能夠識別由於缺少所需Cookie而阻止用戶身份驗證的情況。 在這些情況下，庫會觸發特定錯誤回調 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference)，它被傳回到啟用了Adobe Primetime身份驗證的網站，以便用作指示用戶採取可減輕問題的措施的信號。 為了從這一機制中獲益，網站必須實施 [錯誤報告](/help/authentication/error-reporting.md) 規範。

* 對於AccessEnabler JavaScript SDK v2（2.x版），庫不提供上述機制，因此，在指示用戶採取措施緩解此問題時，無法向啟用Adobe Primetime身份驗證的網站發出信號。

* 可減輕上述問題的行動清單 **適用於所有三個版本** AccessEnabler JavaScript SDK中的。

* 當 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) 實施者網站收到錯誤回調，應指示用戶禁用智慧跟蹤預防(ITP)並啟用第三方cookie，方法是：

* 對於MacOS X High Sierra及更高版本：正在取消選中「」**防止跨站點跟蹤**「 」選項&#x200B;**網站跟蹤**»在瀏覽器的「隱私」頁籤的「首選項」中輸入，如下圖所示。

   ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* 對於MacOS X Sierra和以前版本：正在檢查&quot;**始終允許**&quot;選項&#x200B;**Cookie和網站資料**»在瀏覽器的「隱私」頁籤的「首選項」中輸入，如下圖所示。

   ![](assets/always-allow-safari11.png)

## 野生動物園12 {#safari12}

**詳細資訊**

>[!IMPORTANT]
>
>Safari 10節和Safari 11節的上述所有詳細資訊在Safari 12的情況下仍然適用。

本節詳細介紹 **AccessEnabler JavaScript SDK版本4.x** 12號野生動物園。

>[!NOTE]
>
>請記住，在AccessEnabler JavaScript SDK版本2.x和AccessEnabler JavaScript SDK版本3.x的情況下，它們都使用第三方Cookie進行身份驗證過程，而且由於從Safari 11開始的ITP和第三方Cookie策略，用戶的身份驗證體驗可能是意外和未定義的，從無法登錄到比預期的短持續時間。


### Safari 12上AccessEnabler JavaScript SDK v4（4.x版）的認證功能 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **驗證** 即使用戶的瀏覽器禁用了第三方cookie，使用用戶交互的流也始終有效，因為從4.0版開始，AccessEnabler JavaScript SDK不再使用第三方cookie進行身份驗證。

>[!NOTE]
>
>用戶必須與站點進行交互以開啟登錄彈出窗口和/或與MVPD登錄頁進行交互。

* **授權/印前檢查/用戶元資料** 如果用戶已經經過身份驗證，則操作將完全正常。

### Safari 12上AccessEnabler JavaScript SDK v4（4.x版）的已知問題 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO和SLO

   * 由於從Safari 10開始在Safari中實現localStorage，因此JS SDK無法再通過公共域iFrame共用登錄狀態。 這意味著用戶需要登錄使用AccessEnabler JavaScript SDK的每個站點。 註銷也不會刪除站點間的驗證令牌，因此用戶需要從每個啟用Adobe Primetime驗證的網站註銷。

* 臨時通過

   * 對於臨時傳遞，AccessEnabler JavaScript SDK使用個性化機制，以將驗證令牌鎖定到特定設備（瀏覽器實例）。 由於Safari 12中設計了新的防止跟蹤的機制，我們正在計算和使用的指紋在個性化機制中 **對於具有相同IP地址的所有用戶都是相同的**。 我們確實考慮了客戶端IP以用於個性化目的，但即便如此，這也會對共用相同公共IP地址的用戶產生影響。 對於這些用戶，我們將計算相同的個性化id，並將臨時通行與其綁定。 這意味著，一旦此類用戶使用臨時通行證，其他人將無權訪問它\! 這會對使用NAT或公共代理訪問Internet的多個用戶的公司用戶、教育機構或任何其他組織產生影響。

>[!NOTE]
>
>僅當實施者由於用戶交互而使用臨時通過時，此問題才會影響用戶，否則臨時通過驗證會受到 **自動流** 下。

* 自動流

   * 使用JS SDK 4.0時，在自動模式下嘗試的身份驗證流在沒有任何用戶交互的情況下在Safari 12中不會成功。請注意，即將推出的JS SDK 4.1通過自動流解決了所有問題。

使用受此問題影響的案例：

* 自動TempPass（免費預覽）驗證 — 對於此類流，SDK將引發N130錯誤。

* 被動身份驗證（無提示失敗） — 要求用戶選擇此MVPD並輸入憑據

### 緩解 {#mitigation-safari12}

**SSO和SLO**

在編寫本文時，沒有已知的緩解措施或可能的緩解措施。 Apple在Safari 12中引入了「儲存訪問API」(`https://webkit.org/blog/8124/introducing-storage-access-api`)，但當前實現不適用於localStorage，而僅適用於cookie。 此外，API需要用戶交互才能被使用，而且一旦您使用它，系統還會提示用戶使用與下面類似的權限對話框。

![](assets/permission-dialog-apple.png)


此時，這些Safari要求/提示與我們的UX要求不一致，而且我們沒有像其他瀏覽器那樣的一致行為，在公共域localStorage中保存令牌後，SSO「就能工作」。

**臨時通過**

為了緩解個性化問題並進行用戶交互，我們建議您使用 **[促銷臨時通行證 ](/help/authentication/promotional-temp-pass.md)** 以交互方式提供關於用戶的至少一個附加資訊（例如，電子郵件地址）。

## 野生動物園13 {#safari13}

**詳細資訊**

>[!IMPORTANT]
>
>從Safari 10節到Safari 12節的所有上述詳細資訊在Safari 13的情況下仍然適用。


從Safari 13開始，瀏覽器將對 [智慧跟蹤防範](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP)，在將第三方Cookie標籤為跟蹤Cookie的過程中，使機制背後的啟發式規則更加嚴格，以防止跨站點跟蹤。

如前幾節所述，當實施者使用AccessEnabler JavaScript SDK v2（版本2.x）和AccessEnabler JavaScript SDK v3（版本3.x）時，Adobe Primetime認證服務使用並依賴第三方Cookie作為驗證進程的一部分。 與ITP花費一段時間後開始使用的早期版本Safari瀏覽器相比，Safari 13瀏覽器從開始的第三方Cookie中屏蔽，後者被視為在客戶端 — 伺服器模型通信中跟蹤Cookie。

總之，Safari 13瀏覽器的用戶很可能無法在啟用了Adobe Primetime身份驗證的網站上啟動新身份驗證，該網站使用的是舊版本的AccessEnabler JavaScript SDK、v2（2.x版）或v3（3.x版）。 這是由於所有必需的Adobe的黃金時段身份驗證服務Cookie被ITP阻止，因此使服務無法滿足身份驗證請求。

AccessEnabler JavaScript SDK v4（4.x版）庫不使用第三方Cookie進行身份驗證過程，因此Safari 13更改不會對其操作產生任何影響。

### 緩解 {#mitigation-safari13}

首先，我們強烈建議 **遷移到AccessEnabler JavaScript SDK版本4.x** 在Safari瀏覽器上具有穩定且可預測的行為。

其次，對於AccessEnabler JavaScript SDK v3（3.x版），庫包含一種機制，能夠識別由於缺少所需Cookie而導致用戶身份驗證被阻止的情況。 在這些情況下，庫會觸發特定錯誤回調([N130](/help/authentication/error-reporting.md#advanced-error-codes-reference))，該檔案被傳遞回啟用了Adobe Primetime身份驗證的網站，以作為指示用戶採取可減輕問題的措施的信號。 為了從這一機制中獲益，網站必須實施 [錯誤報告](/help/authentication/error-reporting.md) 規範。

對於AccessEnabler JavaScript SDK v2（2.x版），庫不提供上述機制，因此，在指示用戶採取措施緩解此問題時，無法向啟用Adobe Primetime身份驗證的網站發出信號。

當 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) 實施者網站收到錯誤回調，應指示用戶禁用智慧跟蹤預防(ITP)並啟用第三方cookie，方法是：

* 對於MacOS X High Sierra及更高版本：正在取消選中「」**防止跨站點跟蹤**「 」選項&#x200B;**網站跟蹤**»在瀏覽器的「隱私」頁籤的「首選項」中輸入，如下圖所示。

   ![](assets/prvnt-cross-site-tr-safari13.png)

* 對於MacOS X Sierra和以前版本：正在檢查</span>&quot;**始終允許**&quot;選項&#x200B;**Cookie和網站資料**»在瀏覽器的「隱私」頁籤的「首選項」中輸入，如下圖所示。

   ![](assets/always-allow-safari13.png)
