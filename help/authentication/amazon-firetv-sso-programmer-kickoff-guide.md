---
title: Amazon fireTV SSO — 程式設計師啟動指南
description: Amazon fireTV SSO — 程式設計師啟動指南
exl-id: cf9ba614-57ad-46c3-b154-34204b38742d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# Amazon fireTV SSO — 程式設計師啟動指南 {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 簡介 {#intro}

本檔案說明整合新所需的資訊 **Adobe Primetime驗證的fireTV SDK** 在您的fireTV應用程式中。 此新SDK運用Amazon的fireTV平台上的作業系統層級整合，因此提供 **單一登入** 支援。 若要從單一登入中獲益，您需要花費一些心力，將應用程式從無使用者端API移轉到新的fireTV SDK。 驗證流程有一些變更，詳見下文。

## 高階架構與作業系統層級的整合 {#high}

為了在Amazon fireTV平台上的TV Everywhere應用程式之間達成單一登入，以及改善此平台的整體體驗，我們決定在fireTV OS層級整合我們的核心SDK。 程式設計師必須根據Adobe提供的存根程式庫進行編譯。 實際功能將由Amazon的fireTV OS中的Adobe程式庫提供。

在Amazon提供FireTV模擬器，在作業系統層級整合我們的程式庫之前，只能使用真正的FireTV裝置進行開發。

## 優點 {#bene}

* 在Amazon fireTV平台上所有Adobe支援的TV Everywhere應用程式與所有整合式MVPD之間使用單一登入。
* 能夠從HBA中獲益（搭配支援的MVPD）。
* 可使用最新的fireTV SDK，而不需在每次發行新SDK版本時更新您的應用程式。
* 所有TVE應用程式都可藉由使用共用系統程式庫而獲益，因為您不再需要擁有AccessEnabler程式庫的本機復本。 這麼做也能確保所有應用程式都使用相同的SDK版本。
* 單熒幕驗證 — 不需要註冊代碼和第二熒幕工作流程。

## 從無使用者端API型應用程式移轉至FireTV SDK型應用程式 {#migra1}

若要從無使用者端API移轉至fireTV SDK，您必須移除與無使用者端API相關的程式碼基底，並整合新的fireTV SDK。

相較於無使用者端API應用程式，新的fireTV SDK將驗證移至第一個畫面，不再需要第二個畫面驗證。

這要求程式設計師將MVPD選擇器新增至其應用程式中，讓使用者能夠直接在fireTV裝置上選擇其電視提供者。 選取MVPD後，使用者將會在fireTV裝置上看到MVPD登入頁面。

說明fireTV上一般、HBA和SSO情況的使用者流程線框可在以下網址找到： [Amazon Fire TV - MVVPD登入使用者流程](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## 從以Android SDK為基礎的應用程式移轉至FireTV SDK為基礎的應用程式 {#migra2}

這個新的fireTV SDK與我們現有的Android SDK及目前擁有的檔案非常類似 **整合我們的Android SDK** <!--http://tve.helpdocsonline.com/android-technical-overview-->在我們準備好fireTV SDK檔案之前都可使用。 如果您已有使用我們Android SDK的Android應用程式，則在fireTV應用程式中整合fireTV SDK應該會很簡單。

和現有的Android SDK相比，在fireTV SDK上開發驗證程式會更簡單，因為管理/展示MVPD登入頁面和擷取AuthN權杖的任務會由AccessEnabler程式庫在內部執行。

## 常見問答 {#faq}

1. 如何 **SSO** 工作？

   * SSO適用於採用Adobe Primetime驗證(在同一Amazon fireTV裝置上使用新的fireTV SDK)的所有程式設計人員應用程式
   * 在無使用者端REST API上實作的程式設計人員應用程式與在fireTV SDK上實作的應用程式之間的SSO **將不受支援**

1. fireTV SSO的MVPD涵蓋範圍為何？

   * **所有MVPD** fireTV SDK技術上支援Adobe Primetime驗證整合的SSO。

1. 除了使用新SDK外，還有 **工作流程變更** 程式設計師應該注意嗎？

   * 程式設計師需要實作fireTV平台的MVPD選擇器。

1. 驗證是否有任何變更 **TTL**？

   * 關於驗證TTL的行為沒有改變。
   * 第一個有效的驗證Token將用於執行SSO，在此情況下，將透過SSO驗證的所有其他應用程式將使用相同的TTL，直到它過期為止。 因此，從一個應用程式導覽至另一個應用程式時，第二個應用程式會共用第一個驗證之應用程式的TTL。

1. 如何 **降級API** 工作？

   * 降級API不需要變更，使用者體驗將會與Android裝置上相同。

1. 如何 **暫時傳遞** 流量會受到影響？

   * TempPass流程是單一熒幕，且行為與任何其他原生裝置相同。

1. 其他Adobe功能會如以前般運作嗎？

   * 所有Primetime驗證功能都將在FireTV上運作，就像Android裝置上一樣。
