---
title: MVPD直接整合計畫
description: MVPD直接整合計畫
exl-id: 6423cc9a-a45a-4cde-b562-4cb72c98e505
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# MVPD啟動指南：MVPD直接整合計畫 {#mvpd-dir-int-plan}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#mvpd-kickstart-intro}

歡迎使用Adobe Primetime認證的TV Everywhere。  我們期待與你合作。

>[!NOTE]
>
>這是多通道視頻寫程式分發器(MVPD)的Kickstart指南。 如果您是程式設計師（內容提供商），請參閱 [程式設計師Kickstart指南](/help/authentication/programmer-kickstart-guide.md)。

Zendesk上的黃金時段認證票證系統隨時提供支援。 您也可以從中找到我們流程的示例、文檔和視頻教程。 為了使用 [森德克](https://adobeprimetime.zendesk.com/)，您必須在https://tve.zendesk.com/home註冊並建立帳戶。 您可以註冊的用戶數量以及查看或發佈歸檔票證評論的用戶數量沒有限制。 所有支援問題均應解決：adobe.com上的tve支援

**團隊聯繫人**:

**支援**  — 對於所有問題、事件或功能請求 **tve-support@adobe.com**。

## 1。啟動會議 {#kickoff-meetings}

這些會議的範圍是Adobe與MVPD之間開始技術討論。 在此階段，需要雙方共用檔案。 作為後續工作，Adobe需要在我們的票務系統(https://tve.zendesk.com/)中開啟票證，以跟蹤整合的狀態。

## 2.功能 {#features}

Adobe將設定每週狀態調用，以討論和跟蹤整體整合的時間表、步驟、時間表和實施詳細資訊。 在此階段，Adobe將審查MVPD的規範。 此結果應是一個規範頁，詳細列出MVPD所需的所有功能。 MVPD將發送規範文檔，詳細描述MVPD的驗證/授權實現。

要澄清的項目，請參閱 [MVPD整合功能](/help/authentication/mvpd-integr-features.md)。

此時需要詳細描述以下幾種設定：

* **MVPD的徽標URL**  — 此檔案具有以下尺寸：112 x 33像素。 當用戶按一下「登錄」按鈕選擇付費電視提供商時，程式設計師會在其網站上顯示徽標。
* **TTL（生存時間）值** - TTL通常由MVPD在驗證/授權過程中設定。 但是，Adobe可以覆蓋這些TTL值，並根據程式設計師和MVPD都同意的內容提供不同的值。
* **顯示名稱**  — 當用戶按一下「登錄」按鈕以選擇付費電視提供商時，程式設計師會在其網站上顯示此資訊。
* **Test憑據**  — 兩個配置檔案（暫存和生產）都應具有test憑據清單。

>[!IMPORTANT]
>
>每次用戶啟動權利流時，他都會與單個不透明、唯一的用戶ID關聯。  用戶ID用於標識程式設計師應用的用戶，但來自MVPD。

>[!CAUTION]
>
>每個MVPD的重要通知：用戶ID不應包含任何PII（個人身份資訊）、可自行使用的資訊或可與其他資訊一起用於識別、聯繫或查找用戶。

## 2.元資料交換 {#metadata-ex}

雙方需要交換所有相關環境（生產、轉移等）的元資料。

* **Adobe**
   * 對於轉移環境Adobe的SP元資料，可從以下位置檢索： [驗證暫存sp元資料](https://sp.auth-staging.adobe.com/sp/metadata)
   * 對於生產環境Adobe的SP元資料，可從以下位置檢索： [驗證生產sp元資料](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * 添加元資料（暫存/生產）。

## 4.允許IP清單 {#allow-ip-list}

以下IP應在MVPD的防火牆中白列出。 請與Adobe聯繫以獲取IP清單。

* 黃金時段驗證要求在埠80和443上開啟防火牆，以允許訪問受限資源。

* MVPD需要為驗證和授權伺服器添加IP地址清單（如果是這樣）。

## 5.開發 {#deve}

開發階段的持續時間，將在審查規格後，考慮雙方簽署的項目後確定。 Adobe需要為授權部分編寫自定義代碼。

>[!NOTE]
>
>請注意，授權是按資源執行的。 授權事務通常使用ID字串執行，該ID字串從程式設計師站點傳遞，表示用戶請求授權的通道。 此資源ID在程式設計師和MVPD之間建立，並可根據需要進行粒度化。

## 6。Adobe環境 {#adobe-env}

Adobe為開發過程的不同階段提供不同的環境：

* **資格預審** (PRE-QUAL):PRE-QUAL環境包含下一個發佈候選。 Adobe在將整合升級到發行環境之前，首先在此環境中整合了新的合作夥伴。 合作夥伴有兩週時間在PRE-QUAL環境上test，並且必須明確請求對PRE-QUAL配置進行任何更改(請與Adobe代表聯繫，瞭解有關更改請求流程的詳細資訊)。 錯誤修復會觸發此環境中的新部署。
* **發佈** （發佈）:Adobe當前的生產構建部署到此處的活動環境中。

有關如何使用Adobe環境的詳細資訊，請參見 [瞭解Adobe環境](/help/authentication/understanding-the-adobe-environments.md)

## 7。暫存部署 {#stag-env}

基於從MVPD接收的元資料，Adobe將在Mogini時驗證系統中建立和配置新的MVPD。 這將部署在Adobe的預定試運行環境中，並將配置我們的test程式設計師（測試分發伺服器）。

MVPD需要在其QA/暫存/test環境中執行相同的部署。

## 8.Test和故障排除 {#tes-troubleshoot}

在此階段，Adobe和MVPDtest並排除整合故障。 為了幫助test整合，黃金時段身份驗證團隊可以使用Adobe的APItest站點。 要瞭解有關使用Adobe的APItest站點的詳細資訊，請參閱 [TestAdobeAPItest站點的認證和授權流](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md)。

測試和故障排除成功結束後，將在Adobe的版本轉移環境中啟用整合。 此時，Adobe可以將MVPD與實際程式設計師整合。

## 9。生產部署 {#prod-dep}

* MVPD需要首先在生產配置檔案中部署，以便test連接。

* Adobe在準生產中進行部署。

* 現在，所有各方都可以在生產配置檔案中test。

* 如果此時一切正常，Adobe可將整合移到所有用戶都可使用的發行生產環境（「即時」）。

## 10.升級過程 {#esc-proc}

一旦整合投入生產，提供最佳客戶體驗就至關重要。 為確保在出現伺服器停機問題時作出最佳響應，MVPD必須提供上報過程文檔，以說明提請Adobe注意的問題。

反過來，Adobe為MVPD提供最新的黃金時段身份驗證升級過程。


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
