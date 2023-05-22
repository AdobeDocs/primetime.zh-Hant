---
title: 基於家庭的TV Everywhere認證
description: 基於家庭的TV Everywhere認證
exl-id: abdc7724-4290-404a-8f93-953662cdc2bc
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---

# 基於家庭的TV Everywhere認證

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 什麼是基於家庭的身份驗證？ {#whatis-home-based-authn}

基於家庭的身份驗證(HBA)是一種TV Everywhere功能，它使付費電視用戶在家時無需輸入MVPD憑據即可線上查看電視內容，從而顯著改善了身份驗證流的用戶體驗。

開放認證技術委員會(OATC)基於家庭的認證定義：&quot;家庭內自動驗證是MVPD/OVD使用家庭網路的特徵（或家庭網路上設備之間可自動訪問的標識符）來驗證與家庭網路關聯的訂戶帳戶的過程，因此用戶在建立TVE會話以訪問TVE受保護內容時不需要手動輸入憑據。&quot;



有關HBA和行業標準的詳細資訊，請閱讀 [OATC使用案例和要求](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} 文檔和 **HBA的OATC用戶體驗指南**。

>[!NOTE]
>
>某些HBA流是「高級工作流」包的一部分。 如果有興趣使用此功能，請與您的黃金時段銷售代表聯繫。

## 為什麼HBA對您很重要 {#why-hba}

HBA很重要，因為它實際上為您的查看者消除了登錄障礙，這些查看者在家中並且已經有電纜訂閱。 此外，基於家庭的身份驗證可以顯著提高觀眾的參與度，並為您的TV Everywhere內容提供更好的用戶體驗。

目前，幾乎一半的登錄嘗試都不成功。

一旦HBA被前5個MVPD之一激活，其身份驗證轉換率 **增加了四成** （從45%到63%）

![](assets/authn-conv-pre-post.png)

此外，在下面，您還可以看到與不同MVPD整合的通道的登錄轉換率：為其啟用HBA的HBA和沒有HBA的HBA。 具有HBA的轉換率比沒有HBA的要高得多。

![](assets/hba-vs-non-hba.png)

在為與此MVPD整合的大多數頻道啟用HBA六個月後，我們注意到獨立用戶增加了82%（通過此MVPD訪問TV Everywhere頻道的用戶數幾乎翻了一番）。

2w3相反，如下圖所示，其他未啟用HBA的MVPD在過去6個月中的唯一用戶數量僅增加了26%。

![](assets/unique-visitors-incr.png)

從我們在啟用HBA前6個月和啟用HBA後6個月收集到的資料中，我們發現，查看者對已啟用HBA的渠道的參與度大幅增加。 實際上，啟用HBA的MVPD用戶觀看的內容比未啟用HBA的MVPD用戶平均多30%。

![](assets/user-engagement-increase.png)

## 黃金時段身份驗證HBA支援 {#auth-hba-support}

本節介紹黃金時段驗證提供的HBA支援、黃金時段驗證平台在HBA流中的行為，並提供對實施HBA有用的技術詳細資訊。

支援HBA的黃金時段身份驗證功能

* 能夠為HBA與非HBA身份驗證設定不同的身份驗證TTL（還需要MVPD支援）
* 如果驗證過期，可以自動選擇MVPD（跳過MVPD選取器）。 這非常有用，特別是當HBA TTL較小時。
* 如果驗證是否為HBA，則能夠向程式設計師公開（還需要MVPD支援）

### 黃金時段身份驗證平台上的HBA用戶體驗 {#hba-user-exp}

下表提供了在啟用HBA和未啟用HBA時支援的平台的用戶體驗的資訊：

| 用戶流 — 平台類型 | swf,iOS，安卓 |
|---|---|
| 啟用HBA時 | 當用戶在家時，他們會自動進行身份驗證。 在HBA AuthN令牌過期後，用戶將自動重新進行身份驗證。 |
| 沒有HBA | 用戶被要求選擇其MVPD並輸入其憑據，即使他們在家中。AuthN令牌過期後，用戶必須再次輸入其憑據。 |

| 用戶流 — 平台類型 | js, Windows（本機） |
|---|---|
| 啟用HBA時 | 當用戶在家時，他們會自動進行身份驗證。 在HBA AuthN令牌過期後，用戶必須從選取器中重新選擇其MVPD，並將自動進行身份驗證。 |
| 沒有HBA | 用戶被要求選擇其MVPD並輸入其憑據，即使他們在家。 AuthN令牌過期後，用戶必須再次輸入其憑據。 |

| 用戶流 — 平台類型 | 無客戶端REST API（第二螢幕驗證） |
|---|---|
| 啟用HBA時 | 當用戶在家中並且正在使用無客戶端REST API應用時，在輸入註冊代碼並選擇其MVPD後，他們將在第二螢幕設備上自動進行身份驗證。 在HBA AuthN令牌過期後，用戶將自動重新驗證（在第二螢幕設備上）。 |
| 沒有HBA | 用戶被要求選擇其MVPD並輸入其憑據，即使他們在家。 AuthN令牌過期後，用戶必須再次輸入其憑據。 |

### 實施HBA的技術詳情 {#tech-details-hba}

#### OAuth 2.0協定 {#oauth-2-protocol}

在與OAuth 2.0身份驗證協定整合的MVPD的HBA流中，MVPD發出刷新令牌，Adobe發出HBA身份驗證令牌：

* 刷新令牌具有由MVPD的業務要求確定的TTL。
* HBA驗證令牌TTL **必須小於或等於** 刷新令牌TTL。


*OAuth 2.0協定的HBA身份驗證流描述*


| 用戶操作 | 系統操作 |
|---|---|
| 用戶導航到程式設計師站點。 嘗試播放視頻時，將顯示MVPD選取器。 用戶選擇其MVPD並按一下登錄。 | 進行背景檢查。 MVPD應用其規則集來用於用戶檢測(例如，將用戶的IP地址與分銷商預配調制解調器或寬頻連接機頂盒的MAC地址進行映射)。 |
| 將顯示一個螢幕，該螢幕持續大約3秒。 可以顯示填隙頁，通知用戶通過使用其MVPD帳戶自動登錄。 | <ol><li>安裝在程式設計師端的AccessEnabler將身份驗證請求（作為HTTP請求）發送到Adobe Primetime身份驗證終結點。</li><li>黃金時段驗證終結點將請求重定向到MVPD驗證終結點。 <br />**注：** 請求包含 `hba_flag` 參數（嘗試HBA = true），表示MVPD應嘗試HBA身份驗證。</li><li>MVPD驗證終結點向Adobe Primetime驗證終結點發送授權代碼。</li><li>Adobe Primetime身份驗證使用授權代碼從MVPD的令牌端點請求刷新令牌和訪問令牌。</li><li>MVPD發送驗證決策， `hba_status` (true/false)參數 `id_token`。</li><li>發送對MVPD用戶配置檔案終結點的調用以公開 [hba_status用戶元資料中的鍵](/help/authentication/user-metadata-feature.md#obtaining)。</li><li>MVPD將刷新令牌TTL設定為MVPD同意的值，Adobe將AuthN令牌TTL設定為小於或等於刷新令牌值的值。</li></ol> |
| 用戶已經過身份驗證，現在可以瀏覽有「TV Everywhere」（電視無處不在）內容。 | 驗證令牌將傳遞給現在可以成功瀏覽程式設計師站點的用戶。 |

#### SAML協定 {#saml-protocol}

SAML驗證協定的HBA驗證流描述

| 用戶操作 | 系統操作 |
|---|---|
| 用戶導航到程式設計師站點。 嘗試播放視頻時，將顯示MVPD選取器。 用戶選擇其MVPD並按一下登錄。 | 進行背景檢查。 MVPD應用其規則集來用於用戶檢測(例如，將用戶的IP地址與分銷商預配調制解調器或寬頻連接機頂盒的MAC地址進行映射)。 |
| 將顯示一個螢幕，該螢幕持續大約3秒。 可以顯示填隙頁，通知用戶通過使用其MVPD帳戶自動登錄。 | <ol><li>安裝在程式設計師端的AccessEnabler將身份驗證請求（作為HTTP請求）發送到Adobe Primetime身份驗證終結點。</li><li>黃金時段驗證終結點將請求重定向到MVPD驗證終結點。</li><li>MVPD應以應包含HBA標誌的SAML響應形式發送身份驗證決定：hba_status(true/false)。</li><li>發送對MVPD用戶配置檔案終結點的調用以公開 [hba_status用戶元資料中的鍵](/help/authentication/user-metadata-feature.md#obtaining)。</li></ol> |
| 用戶已經過身份驗證，現在可以瀏覽有「TV Everywhere」（電視無處不在）內容。 | 驗證令牌將傳遞給現在可以成功瀏覽程式設計師站點的用戶。 |


## 如何激活HBA {#how-to-activate-hba}

* **OAuth協定：**
   * 有關啟用HBA的資訊，請參見 [《 Mighine TVE Dashboard使用手冊》](/help/authentication/tve-dashboard-user-guide.md)
* **SAML協定：** 基於家庭的身份驗證在MVPD端激活。 程式設計師或Adobe不需要執行任何操作。
有關支援基於家庭的身份驗證的MVPD的詳細資訊，請參見 [MVPD的HBA狀態](/help/authentication/hba-status-mvpds.md)。

## 常見問題 {#faqs}


**問：** 為什麼使用SAML和OAuth2協定將基於家庭的身份驗證分離？

**答案：** HBA流對於這兩種協定是不同的。 從程式設計師的角度看，無需執行任何操作來確保HBA已為SAML MVPD啟用，而對於OAuth2 MVPD,HBA可以在黃金時段TVE儀表板中切換開啟或關閉。



**問：** 在啟用HBA時，用戶是否需要在首次進行身份驗證時填寫用戶名和密碼？

**答案：** 不需要，不需要用戶名和密碼。



**問：** 如何強制實施家長控制？

**答案1:** Adobe可以禁用HBA以與需要家長控制批准的渠道進行整合。

**答案2:** Adobe正在與OATC合作編寫一份UX文檔，該文檔建議如何使用家長控制設定HBA體驗。



**問：** 支援HBA的提供程式是否具有較短的TTL窗口（用於HBA），而它們是否具有較短的常規身份驗證窗口？

**答案：** TTL設定是可配置的。 我們建議為HBA身份驗證令牌設定較短的TTL，以防止錯誤處理。


## 有用資訊 {#useful-info}

* [即時訪問(HBA)Recommendations](http://www.ctamtve.com/instantaccess){target=_blank}  — 由CTAM
* [在程式設計師應用程式上實現HBA的示例](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/HBA_Flow_Sample.pdf?dc=201604222139-1346){target=_blank}  — 按Adobe
   <!--* [Home Based Authentication User Experience Guidelines for TV Everywhere](http://oatc.us/Standards/DownloadRecommendedPractices.aspx){target=_blank} - by OATC-->
* [基於家庭的身份驗證使用案例和要求](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} 按OATC
* [基於家庭的身份驗證資訊圖](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640){target=_blank}  — 按Adobe
* [使用OAuth 2.0協定進行身份驗證](/help/authentication/authn-oauth2-protocol.md)
* [使用SAML MVPD進行身份驗證](/help/authentication/authn-usecase.md)
* [《 Mighine TVE Dashboard使用手冊》](/help/authentication/tve-dashboard-user-guide.md)
* [hba_status用戶元資料](/help/authentication/user-metadata-feature.md#obtaining)
