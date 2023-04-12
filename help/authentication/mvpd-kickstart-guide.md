---
title: MVPD直接整合計畫
description: MVPD直接整合計畫
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# MVPD啟動指南：MVPD直接整合計畫 {#mvpd-dir-int-plan}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#mvpd-kickstart-intro}

歡迎使用Adobe Primetime TV Everywhere驗證。  我們期待與您合作。

>[!NOTE]
>
>這是多頻道視訊程式設計經銷商(MVPD)的Kickstart指南。 如果您是程式設計師（內容提供商），請參閱 [程式設計師Kickstart指南](/help/authentication/programmer-kickstart-guide.md).

Zendesk上的Primetime驗證票證系統可隨時提供支援。 您也可以在這裡找到我們程式的範例、檔案和教學課程影片。 為了使用 [曾代克](https://adobeprimetime.zendesk.com/)，您必須在https://tve.zendesk.com/home註冊並建立帳戶。 您可以註冊的用戶數量以及可以查看或發佈歸檔票證的用戶數量沒有限制。 所有支援問題均應解決：adobe.com的tve-support

**團隊聯繫人**:

**支援**  — 適用於所有問題、事件或功能要求 **tve-support@adobe.com**.

## 1.啟動會議 {#kickoff-meetings}

這些會議的範圍是Adobe與MVPD之間開始技術討論。 在這個過程中，需要雙方共用檔案。 隨後，Adobe需要在票務系統(https://tve.zendesk.com/)中開啟票證，以追蹤整合的狀態。

## 2.功能 {#features}

Adobe會設定每週狀態呼叫，以討論及追蹤整合的整體排程、步驟、時間軸和實作詳細資訊。 在此階段，Adobe會檢閱MVPD的規格。 結果應為詳細說明MVPD所需所有功能的規格頁面。 MVPD將發送Adobe規範文檔，詳細說明MVPD的驗證/授權實施。

有待澄清的項目，請參閱 [MVPD整合功能](/help/authentication/mvpd-integr-features.md).

此時需要詳細說明數個設定：

* **MVPD的徽標URL**  — 此檔案具有下列維度：112 x 33像素。 當用戶按一下「登錄」按鈕選擇付費電視提供商時，該徽標由程式設計師在其網站上顯示。
* **TTL（存留時間）值** - TTL通常由MVPD在驗證/授權程式期間設定。 不過，Adobe可以覆寫這些TTL值，並根據程式設計人員和MVPD同意的內容提供不同的值。
* **顯示名稱**  — 當用戶按一下「登錄」按鈕選擇付費電視提供商時，程式設計師會在其網站上顯示此資訊。
* **測試憑證**  — 設定檔（測試和生產）都應包含測試憑證清單。

>[!IMPORTANT]
>
>每次使用者啟動權限流程時，就會將其與單一、不透明且不重複的使用者ID建立關聯。  用戶ID用於標識程式設計師應用的用戶，但源自MVPD。

>[!CAUTION]
>
>每個MVPD的重要通知：使用者ID不應包含任何PII（個人識別資訊）、可單獨使用的資訊，或搭配其他資訊使用，以識別、聯絡或尋找使用者。

## 2.元資料交換 {#metadata-ex}

雙方需要交換所有相關環境（生產、測試等）的中繼資料。

* **Adobe**
   * 對於測試環境Adobe的SP中繼資料，可從以下位置擷取： [驗證中繼sp元資料](https://sp.auth-staging.adobe.com/sp/metadata)
   * 對於生產環境Adobe的SP中繼資料，可從以下位置擷取： [驗證生產sp元資料](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * 新增中繼資料（測試/生產）的方式。

## 4.允許IP清單 {#allow-ip-list}

下列IP應列入MVPD防火牆的白名單。 請聯絡Adobe以取得IP清單。

* Primetime驗證要求在埠80和443上開啟防火牆，以允許訪問受限資源。

* MVPD需要為驗證和授權伺服器新增IP位址清單（若是如此）。

## 5.發展 {#deve}

開發階段的持續時間將在審查規格後，並考慮雙方簽訂的項目後確定。 Adobe需要為授權部分編寫自定義代碼。

>[!NOTE]
>
>請注意，授權是按資源執行。 授權事務通常使用從程式設計師站點傳遞的ID字串執行，該ID字串表示用戶請求授權的通道。 此資源ID在程式設計師和MVPD之間建立，並且可以根據需要盡量精細。

## 6.Adobe環境 {#adobe-env}

Adobe針對開發程式的不同階段提供不同的環境：

* **資格預審** (PRE-QUAL):PRE-QUAL環境包含下一個發行候選版本。 Adobe最初在此環境中整合了新合作夥伴，然後才將整合升級到發行環境。 合作夥伴有兩週時間在PRE-QUAL環境上進行測試，並必須明確要求對PRE-QUAL配置進行任何更改(請與Adobe代表聯繫，以了解有關更改請求過程的詳細資訊)。 錯誤修正會在此環境中觸發新部署。
* **發行** （發行）:Adobe目前的生產組建部署至此處的即時環境。

如需如何使用Adobe環境的詳細資訊，請參閱 [了解Adobe環境](/help/authentication/understanding-the-adobe-environments.md)

## 7.中繼部署 {#stag-env}

Adobe會根據從MVPD收到的中繼資料，在Primetime驗證系統中建立並設定新的MVPD。 這將部署在Adobe的預先測試環境中，並將用我們的測試程式設計師(TestDistributors)進行配置。

MVPD必須在其QA/預備/測試環境中執行相同部署。

## 8.測試和疑難排解 {#tes-troubleshoot}

在此階段中，Adobe和MVPD測試，並疑難排解整合。 為協助測試整合，Primetime驗證團隊可使用Adobe的API測試網站。 若要進一步了解如何使用Adobe的API測試網站，請參閱 [使用AdobeAPI測試網站測試驗證和授權流程](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

測試和疑難排解順利結束時，會在Adobe的發行測試環境中啟用整合。 此時，Adobe可以將MVPD與實際程式設計師整合。

## 9.生產部署 {#prod-dep}

* MVPD必須先在生產設定檔中部署，才能測試連線能力。

* Adobe在準生產環境中部署。

* 所有交易方現在都可以在生產設定檔中測試。

* 如果目前一切正常，Adobe可將整合移至可供所有使用者使用的發行生產環境（「正式啟用」）。

## 10.升級程式 {#esc-proc}

一旦整合上線投入生產，就必須提供最佳客戶體驗。 為了在發生伺服器故障時獲得最佳回應，MVPD必須針對提請Adobe注意的問題提供呈報程式檔案。

接著，Adobe會為MVPD提供最新的Primetime驗證呈報程式。


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
