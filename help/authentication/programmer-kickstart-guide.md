---
title: 程式設計師快速入門手冊
description: 程式設計師快速入門手冊
exl-id: 0aecdb81-9b97-4475-b0b0-654d916b2374
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 程式設計師快速入門手冊 {#programmer-kickstart-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#prog-kickstart-guide-intro}

歡迎使用Adobe Primetime驗證，隨時隨地都能觀賞電視。 我們期待與您合作。

>[!NOTE]
>
>這是程式設計師（內容提供者）的快速入門手冊。 如果您是多頻道視訊程式設計經銷商(MVPD)，請務必參閱 [MVPD快速入門手冊](/help/authentication/mvpd-kickstart-guide.md).


Adobe Primetime驗證連絡人：

* 支援 — 針對所有問題、事件或功能請求， `tve-support@adobe.com`
* 系統會在您的專案啟動時，將啟用連絡人指派給您的專案。

下列資訊概述一些重要的第一步，讓我們開始一個紮實而有效的開始。 我們的目標是要提供有關我們將如何與合作夥伴合作達成整合的說明和期望。 請注意每個專案底下的「您將提供」/「Adobe將會提供」區段。 當我們完成專案時，會以檢查清單或指南的方式列出這些清單。

本檔案假設程式設計師已註冊與選定的MVPD合作夥伴合作。

## 發行排程 {#release-schedule}

已規劃Adobe衝刺開發週期，以便您檢視排程發行的時間，以及如何透過我們的開發系統推廣每個版本。

每個衝刺完成後，即可進行QE，或在UAT伺服器上檢視新的實作。

大約每6週會對Adobe資格預審伺服器發佈一次。 （這是執行最終QE時，我們保留下一個建議版本的伺服器。） 這些組建將包含自上次放置以來在衝刺中完成的所有工作。 目前提供兩週QE視窗，供合作夥伴測試此版本。

假設在前兩週測試時段內未發生任何嚴重問題，此版本將提升至即時生產。 這表示整合可在Adobe發行環境中使用，但合作夥伴會在公開發行時選擇。

<!--For the latest release schedule information, see the Release Calendar.-->

## 支援檔案 {#supp-doc}

Adobe將提供：

* 部署指南： **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* 存取我們的Zendesk客戶支援系統。 您也可以在這裡找到一些程式的範例、資訊和影片教學課程。 若要在Zendesk上存取此檔案，以及張貼在該處的其他檔案，您必須註冊並建立帳戶： `https://tve.zendesk.com/home`. 您可以註冊的使用者數量沒有限制。  您可以檢視並分享任何已歸檔票證的註解。 所有支援問題皆應傳送至 `tve-support@adobe.com`.
* [程式設計師整合指南](/help/authentication/programmer-integration-guide-overview.md)
* 媒體權杖驗證器程式庫： `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## 測試環境設定 {#test-env-setup}

Adobe會先使用Adobe測試網站設定您，在那裡，Adobe會當作MVPD用於測試。 然後，您的團隊可以設定呼叫AdobeAPI的測試網站。 使用預設的MVPD選取器，並選取「Adobe」作為idP。

您將提供：

1. 要求者ID。 這是字串，可唯一識別向Adobe Primetime驗證提出要求的網站或應用程式的品牌。 字串本身是任意的，但需要在Adobe和程式設計師之間商定
1. 頻道資訊。 這是一組字串，可識別請求者ID所請求的內容管道。 在許多情況下，管道和請求者ID會相同。 不過，您可能有多個內容管道，這些管道可由同一ID請求。 頻道名稱字串應該與有線電視頻道相對應。 有些MVPD會透過AuthN和/或AuthZ通訊協定驗證此值。
1. 網域名稱（允許用於該請求者ID）。 這將是一個實際網域名稱的清單，將由Adobe列出以接受請求者ID。 這樣可確保只有您核准的網域才能存取含有您中繼資料的Adobe Primetime驗證。 注意：對生產有效的網域名稱在測試/測試中可能不同，應該提供和識別這兩個名稱。

Adobe將設定帳戶，而Adobe將提供：

* 存取測試網站的登入和密碼

## 使用MVPD設定 {#setup-mvpd}

本節說明從Adobe測試網站移轉至MVPD使用時需要哪些專案。

您將提供（透過MVPD）：

* **兩組認證**：
   * AuthN + AuthZ ：已驗證和授權之使用者的登入/密碼
   * AuthN + Non-AuthZ ：已驗證但未授權之使用者的登入/密碼
* **資源ID**. 這是將會透過AuthZ通訊協定以MVPD驗證的特定內容識別碼。 這可以在頻道、節目、集數或資產層級；應該與您的MVPD商定。

Adobe Primetime驗證支援以MRSS為基礎的中繼資料結構，這表示資源ID可以視需要而具體，並且可以包含特定MVPD特有的識別碼。

**全新MVPD整合**：請務必記住，您選擇的MVPD在完成任何整合時都會發揮不可或缺的作用。 Adobe需要根據每個MVPD的規格為其編寫程式碼。 在完成這些步驟之前，您將無法從對話方塊中選取該MVPD，或完成您的產品測試。 Adobe需要提前排程這項工作，以配合下一個可用的衝刺。 （如需目前排程資訊，請參閱發行行事曆。）

**現有的MVPD整合**：如果您選擇的MVPD已使用Adobe設定，則連線步驟應更簡單（更快），且通常可透過變更設定來達到連線。

>[!NOTE]
>
>MVPD仍需啟用程式設計師，並簽署任何相關的商業交易。

**含MVPD的QE**：所有整合都會涉及聯合QE，而且由於一般使用者最終是MVPD的客戶，因此許多使用者在推送「即時」之前都會設定測試週期。 由於這涉及MVPD資源的排程，因此這是潛在的延遲區域。

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->
