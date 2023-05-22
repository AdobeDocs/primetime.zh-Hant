---
title: 程式設計師啟動指南
description: 程式設計師啟動指南
exl-id: 0aecdb81-9b97-4475-b0b0-654d916b2374
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 程式設計師啟動指南 {#programmer-kickstart-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#prog-kickstart-guide-intro}

歡迎使用Adobe Primetime認證的TV Everywhere。 我們期待與你合作。

>[!NOTE]
>
>這是面向程式設計師（內容提供商）的Kickstart指南。 如果您使用的是多通道視頻節目分發伺服器(MVPD)，請確保 [MVPD啟動指南](/help/authentication/mvpd-kickstart-guide.md)。


Adobe Primetime身份驗證聯繫人：

* 支援 — 針對所有問題、事件或功能請求， `tve-support@adobe.com`
* 在項目啟動時，將為您的項目分配支援聯繫人。

以下資訊概述了一些重要的第一步，以使我們能夠實現可靠而高效的開端。 其目標是就我們將如何與合作夥伴合作以實現整合提供解釋和期望。 請注意下面每個項目的「您將提供」/「Adobe將提供」部分。 這些是通過核對表列出的，或是在我們完成項目時提供的指南。

本文檔假定程式設計師已註冊以與所選MVPD合作夥伴一起工作。

## 發放計畫 {#release-schedule}

Adobe衝刺開發週期已計畫出來，以便您能夠瞭解我們的發佈計畫時間以及每個發佈如何通過我們的開發系統進行推廣。

每次衝刺完成後，都可進行QE，或查看UAT伺服器上的新實施。

大約每6週向Adobe資格預審伺服器發佈一次。 （這是我們在執行最終QE時存放建議的下一版本的伺服器。） 這些生成將包括自上次刪除後在短跑中完成的所有工作。 此時，合作夥伴可使用兩週的QE窗口來test此版本。

假定在前兩週的測試窗口中未出現任何關鍵問題，則將將發佈提升為即時生產。 這意味著整合將在Adobe發行環境中提供，但合作夥伴選擇何時公開發行。

<!--For the latest release schedule information, see the Release Calendar.-->

## 支援文檔 {#supp-doc}

Adobe將提供：

* 部署指南： **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* 訪問我們的Zendesk客戶支援系統。 您也可以在此處找到有關某些進程的示例、資訊和視頻教程。 要在Zendesk上訪問此文檔，以及在其上發佈的其他文檔，您必須在以下位置註冊並建立帳戶： `https://tve.zendesk.com/home`。 您可以註冊的用戶數量沒有限制。  您可以查看並共用任何歸檔票證上的注釋。 所有支援問題均應處理到 `tve-support@adobe.com`。
* [程式設計師整合指南](/help/authentication/programmer-integration-guide-overview.md)
* 媒體令牌驗證器庫： `https://tve.zendesk.com/entries/471323-media-token-validator-library`。

## Test環境設定 {#test-env-setup}

Adobe將首先設定您的Adobetest站點，在該站點中，Adobe將充當MVPD，用於test。 然後，您的團隊可以設定調用testAPI的Adobe網站。 使用預設的MVPD選擇器，然後選擇「Adobe」作為idP。

您將提供：

1. 請求者ID。 這是一個字串，它將唯一標識向Adobe Primetime身份驗證請求的網站或應用程式的品牌。 字串本身是任意的，但需要由Adobe和程式設計師商定
1. 頻道資訊。 這是一組字串，它標識請求者ID請求的內容通道。 在很多情況下，通道和請求者ID是相同的。 但是，您可能有多個通道的內容，這些通道可以由同一ID請求。 頻道名稱字串應與有線電視頻道對應。 某些MVPD將通過AuthN和/或AuthZ協定驗證此值。
1. 域名（該請求者ID允許使用）。 這將是實際域名的清單，該清單將由Adobe列出以接受請求者ID。 這確保只有您的已批准域才有權使用您的元資料存取Adobe Primetime身份驗證。 注：對生產有效的域名可能不同於測試/試運行，應提供並標識兩者。

Adobe將設定帳戶，Adobe將提供：

* 登錄和密碼以訪問test站點

## 使用MVPD進行設定 {#setup-mvpd}

本節介紹從Adobetest站點遷移以使用MVPD時需要什麼。

您將提供（通過MVPD）:

* **兩組憑據**:
   * AuthN + AuthZ :已驗證和授權的用戶的登錄/密碼
   * AuthN +非AuthZ :已驗證但未授權的用戶的登錄/密碼
* **資源ID**。 這是將通過AuthZ協定通過MVPD驗證的特定內容標識符。 這可以在頻道、節目、劇集或資產級別；應與您的MVPD商定。

Adobe Primetime驗證支援基於MRSS的元資料架構，這意味著資源ID可以根據需要是特定的，並且可以包括對特定MVPD唯一的標識符。

**新MVPD整合**:必須記住，您選擇的MVPD在完成任何整合過程中都起著不可或缺的作用。 Adobe需要根據每個MVPD的規格編寫代碼。 在完成這些步驟之前，您將無法從對話框中選擇該MVPD，或完成產品測試。 Adobe需要提前安排這項工作，以適應下一次的短跑。 （有關當前計畫資訊，請參閱「發行日曆」。）

**現有MVPD整合**:如果您選擇的MVPD已使用Adobe設定，則連接步驟應該簡單得多（速度更快），並且通常可以通過配置更改來實現連接。

>[!NOTE]
>
>MVPD仍然必須啟用程式設計師並簽署任何相關的商業協定。

**QE與MVPD**:所有整合都將涉及聯合QE，而且由於最終用戶最終是MVPD的客戶，因此許多企業在推動「即時」之前都設定了test週期。 由於這涉及MVPD資源的調度，因此這是可能的延遲區域。

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->
