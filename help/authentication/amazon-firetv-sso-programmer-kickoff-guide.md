---
title: AmazonFireTV SSO — 程式設計師啟動指南
description: AmazonFireTV SSO — 程式設計師啟動指南
exl-id: cf9ba614-57ad-46c3-b154-34204b38742d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# AmazonFireTV SSO — 程式設計師啟動指南 {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 導言 {#intro}

本文檔介紹了整合新產品所需的資訊 **Adobe Primetime驗證的fireTV SDK** 你的fireTV應用程式。 這種新的SDK利用AmazonfireTV平台上的OS級整合，從而提供 **單一登錄** 支援。 要從單一登錄中獲益，您需要付出一些努力，才能將您的應用程式從無客戶端API遷移到新的fireTV SDK。 驗證流中有一些更改，將在下面詳細說明。

## 高級體系結構和作業系統級整合 {#high}

為了實現AmazonfireTV平台上TV Everywhere應用程式間的單點登錄，並改善該平台的整體體驗，我們決定在fireTV作業系統級整合我們的核心SDK。 程式設計師需要根據Adobe提供的存根庫進行編譯。 實際功能將由AmazonfireTV作業系統中的Adobe庫提供。

在Amazon提供一台fireTV模擬器，將我們的庫整合到作業系統級別之前，只有使用真正的fireTV設備才有可能進行開發。

## 好處 {#bene}

* 在AmazonfireTV平台上所有Adobe供電的TV Everywhere應用程式之間單一登錄所有整合MVPD。
* 能夠從HBA（支援的MVPD）中獲益。
* 能夠使用最新的fireTV SDK，而無需每次發佈新的SDK版本時更新應用程式。
* 所有TVE應用都可以從使用共用系統庫中獲益，因為它不需要擁有AccessEnabler庫的本地副本。 這還可確保所有應用程式都使用相同的SDK版本。
* 單屏驗證 — 無需註冊代碼和第二屏工作流。

## 從基於Clientless API的應用遷移到基於FireTV SDK的應用 {#migra1}

要從無客戶端API遷移到fireTV SDK，您需要刪除與無客戶端API相關的代碼庫，並整合新的fireTV SDK。

與基於Clientless API的應用相比，新的fireTV SDK將驗證移動到第一螢幕，不再需要第二螢幕驗證。

這要求程式設計師將MVPD選取器添加到其應用中，以便用戶可以在fireTV設備上選擇其電視提供商。 選擇MVPD後，用戶將顯示fireTV設備上的MVPD登錄頁。

有關描述fireTV上的常規、HBA和SSO方案的用戶流的無線幀，請訪問 [AmazonFire TV - MVVPD登錄用戶流](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/)。

## 從基於Android SDK的應用遷移到基於fireTV SDK的應用 {#migra2}

此新的fireTV SDK與我們現有的Android SDK以及我們當前為 **整合我們的Android SDK** <!--http://tve.helpdocsonline.com/android-technical-overview-->在fireTV SDK文檔準備好之前，可使用。 如果您已經有使用我們的Android SDK的Android應用程式，則fireTV SDK在fireTV應用程式中的整合應該很簡單。

與現有的Android SDK相比，在fireTV SDK上，驗證過程將更容易開發，因為管理/呈現MVPD登錄頁和檢索AuthN令牌的任務將由AccessEnabler庫在內部執行。

## 常見問題 {#faq}

1. 如何 **SSO** 工作？

   * SSO將可跨所有由Adobe Primetime身份驗證支援的程式設計師應用程式工作，這些程式設計師在同一台AmazonfireTV設備上使用新的fireTV SDK
   * 在無客戶端REST API上實現的程式設計師應用程式與在fireTV SDK上實現的應用程式之間的SSO **不支援**

1. FireTV SSO的MVPD報導是什麼？

   * **所有MVPD** 通過Adobe Primetime驗證整合的fireTV SDK在技術上支援SSO。

1. 除了使用新的SDK外， **工作流更改** 程式設計師應該知道嗎？

   * 程式設計師需要為fireTV平台實現MVPD選取器。

1. 是否對身份驗證進行任何更改 **TTL**?

   * 身份驗證TTL的行為沒有變化。
   * 第一個有效的身份驗證令牌將用於執行SSO，在這種情況下，所有通過SSO進行身份驗證的其他應用程式將使用相同的TTL，直到其過期。 因此，當從一個應用程式導航到另一個應用程式時，第二個應用程式將共用驗證的第一個應用程式的TTL。

1. 如何 **降級API** 工作？

   * 降級API不需要更改，用戶體驗將與Android設備上的相同。

1. 如何 **臨時傳遞** 流是否受到影響？

   * TempPass流是單螢幕，與任何其他本機設備一樣。

1. 其他Adobe功能是否能像以前一樣工作？

   * 所有黃金時段驗證功能在fireTV和Android設備上都可用。
