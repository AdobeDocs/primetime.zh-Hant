---
title: MVPD直接整合計畫
description: MVPD直接整合計畫
exl-id: 6423cc9a-a45a-4cde-b562-4cb72c98e505
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# MVPD快速入門手冊：MVPD直接整合計畫 {#mvpd-dir-int-plan}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#mvpd-kickstart-intro}

歡迎使用Adobe Primetime驗證，隨時隨地都能觀賞電視。  我們期待與您合作。

>[!NOTE]
>
>這是多頻道視訊節目經銷商(MVPD)的快速入門手冊。 如果您是程式設計師（內容提供者），請參閱 [程式設計師的Kickstart指南](/help/authentication/programmer-kickstart-guide.md).

您可以隨時透過Zendesk上的Primetime驗證票證系統取得支援。 您也可以在這裡找到我們程式的範例、檔案和影片教學課程。 為了使用 [Zendesk](https://adobeprimetime.zendesk.com/)，您必須在https://tve.zendesk.com/home註冊並建立帳戶。 您可以註冊的使用者數量，以及可以在歸檔票證上檢視或張貼評論的使用者數量沒有限制。 所有支援問題皆應傳送至： tve-support，網址為adobe.com

**團隊連絡人**：

**支援**  — 針對所有問題、事件或功能要求 **tve-support@adobe.com**.

## 1.啟動會議 {#kickoff-meetings}

這些會議的範圍是Adobe與MVPD之間開始技術性討論。 在這個程式中，檔案需要由雙方共用。 接下來，Adobe需要在我們的票證系統(https://tve.zendesk.com/)中開啟票證，以追蹤整合狀態。

## 2.功能 {#features}

Adobe將設定每週狀態通話，以討論和追蹤整合的整體排程、步驟、時間表和實施詳細資訊。 在此階段中，Adobe會檢閱MVPD的規格。 其結果應該是規格頁面，其中會詳細說明MVPD所需的所有功能。 MVPD會傳送規格檔案給Adobe，詳細說明MVPD的驗證/授權實作。

要釐清的專案，請參閱 [MVPD整合功能](/help/authentication/mvpd-integr-features.md).

目前需要詳細說明幾項設定：

* **MVPD的標誌URL**  — 此檔案的尺寸如下： 112 x 33畫素。 當使用者按一下「登入」按鈕以選擇他們的付費電視提供者時，程式設計師在其網站上顯示標誌。
* **TTL （存留時間）值** - TTL通常由MVPD在驗證/授權程式期間設定。 不過，Adobe可以覆寫這些TTL值，並根據程式設計人員和MVPD雙方同意的內容提供不同的值。
* **顯示名稱**  — 當使用者按一下「登入」按鈕以選取其付費電視提供者時，程式設計師在其網站上會顯示此資訊。
* **測試認證**  — 兩個設定檔（測試和生產）都應該有測試認證清單。

>[!IMPORTANT]
>
>每次使用者啟動權益流程時，他都會與單一、不透明、不重複的使用者ID建立關聯。  使用者ID是用來識別程式設計師應用程式的使用者，但源自MVPD。

>[!CAUTION]
>
>每個MVPD的重要通知：使用者ID不應包含任何PII （個人識別資訊）、可以單獨使用或搭配其他資訊使用的資訊，以識別、聯絡或尋找使用者。

## 2.中繼資料交換 {#metadata-ex}

雙方需要交換所有相關環境（生產、測試等）的中繼資料。

* **Adobe**
   * 中繼環境Adobe的SP中繼資料可從下列位置擷取： [驗證中繼sp中繼資料](https://sp.auth-staging.adobe.com/sp/metadata)
   * 生產環境Adobe的SP中繼資料可從下列位置擷取： [驗證生產sp中繼資料](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * 新增中繼資料（測試/生產）的方式。

## 4.允許IP清單 {#allow-ip-list}

下列IP應在MVPD的防火牆中列入白名單。 請聯絡Adobe以取得IP清單。

* Primetime驗證需要在連線埠80和443上開啟防火牆，以允許存取受限制的資源。

* MVPD需要新增驗證和授權伺服器的IP位址清單（如果情況如此）。

## 5.開發 {#deve}

開發階段的持續時間將在檢閱規格後決定，並考慮雙方簽署的專案。 Adobe需要為授權部分寫入自訂程式碼。

>[!NOTE]
>
>請注意，授權是按資源執行。 授權交易通常使用從程式設計師網站傳遞的ID字串執行，代表使用者請求授權的管道。 此資源ID是在程式設計師和MVPD之間建立，且可視需要提供精細度。

## 6.Adobe環境 {#adobe-env}

Adobe為開發流程的不同階段提供不同的環境：

* **預先資格** （預先測試）：預先測試環境包含下一個候選版本。 Adobe在將整合升級至發行版環境之前，已初步在此環境中整合新合作夥伴。 合作夥伴有兩週的時間可在PRE-QUAL環境中測試，且必須明確要求變更PRE-QUAL設定(請聯絡您的Adobe代表以取得變更要求流程的詳細資訊)。 錯誤修正會在此環境中觸發新部署。
* **版本** （版本）：Adobe目前的生產組建已部署至此處的即時環境。

如需如何使用Adobe環境的詳細資訊，請參閱 [瞭解Adobe環境](/help/authentication/understanding-the-adobe-environments.md)

## 7.中繼部署 {#stag-env}

根據從MVPD收到的中繼資料，Adobe將在Primetime驗證系統中建立和設定新的MVPD。 這將部署在Adobe的預先測試環境中，並將由我們的測試程式設計師(TestDistributors)進行設定。

MVPD需要在其QA/中繼環境/測試環境中執行相同的部署。

## 8.測試與疑難排解 {#tes-troubleshoot}

在此階段，請Adobe和MVPD測試並疑難排解整合。 為協助測試整合，Primetime驗證團隊可以使用Adobe的API測試網站。 若要進一步瞭解使用Adobe API測試網站，請參閱 [使用AdobeAPI測試網站測試驗證和授權流程](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

測試和疑難排解成功完成後，整合會在Adobe的發行預備環境中啟用。 此時，Adobe可以將MVPD與實際的程式設計師整合。

## 9.生產部署 {#prod-dep}

* MVPD必須先部署在生產設定檔中，才能測試連線。

* Adobe會部署在預先準備好的生產環境中。

* 所有各方現在均可在生產設定檔中測試。

* 如果此時一切正常，Adobe可以將整合移至發行版生產環境（「即時」），以供所有使用者使用。

## 10.向上呈報程式 {#esc-proc}

整合一經上線至生產環境，便能提供最佳客戶體驗變得至關重要。 為了在伺服器故障時確保最佳回應，MVPD必須針對提請Adobe注意的問題提供向上呈報程式檔案。

反過來，Adobe會為MVPD提供最新的Primetime驗證提升程式。


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
