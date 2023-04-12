---
title: 程式設計師啟動指南
description: 程式設計師啟動指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# 程式設計師啟動指南 {#programmer-kickstart-guide}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#prog-kickstart-guide-intro}

歡迎使用Adobe Primetime TV Everywhere驗證。 我們期待與您合作。

>[!NOTE]
>
>這是面向程式設計師（內容提供商）的Kickstart指南。 若您使用多頻道視訊程式設計經銷商(MVPD)，請務必查看 [MVPD啟動指南](/help/authentication/mvpd-kickstart-guide.md).


Adobe Primetime驗證聯絡人：

* 支援 — 適用於所有問題、事件或功能要求 `tve-support@adobe.com`
* 在您的專案開始前，會為您的專案指派啟用連絡人。

以下資訊概述了一些重要的第一步，以使我們能夠從一個堅實而高效的開始。 目標是要針對我們如何與合作夥伴合作以達成整合提供說明和期望。 請注意下方每個項目的「you will provide」/「Adobe將提供」章節。 這些會透過檢查清單列出，或在我們完成專案時提供指南。

本檔案假設程式設計人員已註冊，可與所選的MVPD合作夥伴合作。

## 發行排程 {#release-schedule}

Adobe衝刺開發週期已規劃好，讓您了解我們的發行排程時間，以及每個發行如何透過我們的開發系統進行推廣。

每次衝刺完成後，都可進行QE，或在UAT伺服器上查看新實施。

大約每6週向Adobe資格預審伺服器發行一次。 （這是我們在實施最終QE時，提出的下一版的伺服器。） 這些組建將包含自上次放置以來在Sprint中完成的所有工作。 目前，合作夥伴可使用兩週的QE期間來測試此版本。

假設在前兩週的測試期間未發生任何重大問題，則此版本將提升為即時生產。 這表示整合將可在Adobe發行環境中使用，但合作夥伴會在發行公開時選擇。

<!--For the latest release schedule information, see the Release Calendar.-->

## 支援檔案 {#supp-doc}

Adobe將提供：

* 部署指南： **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* 訪問我們的Zendesk客戶支援系統。 您也可以在這裡找到一些程式的範例、資訊和教學課程影片。 為了在Zendesk上訪問此文檔，以及發佈在Zendesk上的其他文檔，您必須在註冊並建立帳戶 `https://tve.zendesk.com/home`. 您可以註冊的使用者數量沒有限制。  您可以查看並分享任何歸檔票證的評論。 所有支援問題均應處理至 `tve-support@adobe.com`.
* [程式設計師整合指南](/help/authentication/programmer-integration-guide-overview.md)
* 媒體令牌驗證程式庫： `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## 測試環境設定 {#test-env-setup}

Adobe會先設定您的Adobe測試網站，Adobe會作為MVPD用於測試用途。 然後，您的團隊可以設定呼叫AdobeAPI的測試網站。 使用預設的MVPD選取器，並選取「Adobe」作為idP。

您將提供：

1. 請求者ID。 這是字串，可唯一識別向Adobe Primetime驗證提出請求的網站或應用程式的品牌。 字串本身是任意的，但需要在Adobe和程式設計師之間達成一致
1. 頻道資訊。 這是一組字串，用以識別要求者ID要求的內容頻道。 在許多情況下，通道與請求者ID相同。 不過，您可能有多個內容頻道，可以透過相同ID來請求。 頻道名稱字串應與有線電視頻道相對應。 有些MVPD會透過AuthN和/或AuthZ通訊協定來驗證此值。
1. 網域名稱（允許用於該請求者ID）。 這將會是實際網域名稱的清單，由Adobe列出以接受要求者ID。 這可確保只有已核准的網域才能存取含有中繼資料的Adobe Primetime驗證。 注意：對於測試/測試而言，對生產有效的網域名稱可能不同，應提供並識別兩者。

Adobe會設定帳戶，而Adobe會提供：

* 登錄和密碼以訪問測試站點

## 使用MVPD進行設定 {#setup-mvpd}

本節說明從Adobe測試網站移轉以搭配MVPD運作時，您需要什麼。

您將提供（透過MVPD）:

* **兩組憑據**:
   * AuthN + AuthZ :已驗證和授權的用戶的登錄/密碼
   * AuthN +非AuthZ :已驗證但未授權的用戶的登錄/密碼
* **資源ID**. 這是特定內容識別碼，將透過AuthZ通訊協定以MVPD驗證。 這可以是頻道、節目、集數或資產層級；應與您的MVPD同意。

Adobe Primetime驗證支援以MRSS為基礎的中繼資料結構，這表示資源ID可視需要而定，並可包含特定MVPD所特有的識別碼。

**新MVPD整合**:請務必記住，您選擇的MVPD在完成任何整合時，都扮演著不可或缺的角色。 Adobe需要根據每個MVPD的規格來編寫程式碼。 在完成這些步驟之前，您將無法從對話方塊中選取該MVPD，或完成產品測試。 Adobe需要提前安排此工作，以適應下一個可用的衝刺。 （如需目前排程資訊，請參閱發行日曆。）

**現有MVPD整合**:如果您選擇的MVPD已通過Adobe設定，則連接步驟應該更簡單（更快），並且通常可以通過配置更改實現連接。

>[!NOTE]
>
>MVPD仍然必須啟用程式設計師，並簽收任何相關的商業交易。

**QE與MVPD**:所有整合都將涉及聯合QE，而由於使用者最終是MVPD的客戶，因此許多使用者在推送「上線」前已設定測試週期。 由於這涉及MVPD資源的排程，因此這是可能的延遲區域。

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->

