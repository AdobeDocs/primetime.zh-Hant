---
title: Amazon fireTV SSO — 程式設計師啟動指南
description: Amazon fireTV SSO — 程式設計師啟動指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Amazon fireTV SSO — 程式設計師啟動指南 {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 簡介 {#intro}

本檔案說明整合新 **Adobe Primetime驗證的fireTV SDK** 在fireTV應用程式中。 此新SDK充分運用Amazon之fireTV平台上的作業系統層級整合，因此提供 **單一登入** 支援。 若要從單一登入中獲益，您需先花點心力，將應用程式從無用戶端API移轉至新的fireTV SDK。 驗證流程中有一些變更，將於下文詳細說明。

## 高級體系結構和作業系統級整合 {#high}

為了在Amazon fireTV平台上實現TV Everywhere應用程式間的單一登入，並改善此平台上的整體體驗，我們決定在fireTV OS層級整合核心SDK。 程式設計師需要根據Adobe提供的存根庫進行編譯。 實際功能將由Amazon fireTV OS中存在的Adobe程式庫提供。

在Amazon提供fireTV模擬器，將程式庫整合至作業系統層級之前，開發只能使用真正的fireTV裝置。

## 優點 {#bene}

* 在Amazon fireTV平台上的所有Adobe供電的TV Everywhere應用程式與所有整合的MVPD之間單一登入。
* 能夠從HBA中受益（支援的MVPD）。
* 每次發行新SDK版本時，都無須更新應用程式，即可使用最新的fireTV SDK。
* 所有TVE應用程式都可通過使用共用系統庫而獲益，無需擁有AccessEnabler庫的本地副本。 這也可確保所有應用程式都使用相同的SDK版本。
* 單螢幕驗證 — 不需要註冊代碼和第2螢幕工作流程。

## 從無用戶端API型應用程式移轉至fireTV SDK型應用程式 {#migra1}

若要從無用戶端API移轉至fireTV SDK，您需要移除與無用戶端API相關的程式碼基底，並整合新的fireTV SDK。

與基於無用戶端API的應用程式相比，隨著新的fireTV SDK，驗證會移至第一個畫面，不再需要第二個畫面驗證。

這要求程式設計人員在其應用程式中新增MVPD選擇器，讓使用者能直接在fireTV裝置上挑選其電視提供者。 選取MVPD時，使用者會在fireTV裝置上顯示MVPD登入頁面。

有關FireTV上常規、HBA和SSO方案的用戶流的線框，請參見 [Amazon Fire TV - MVVPD登入使用者流程](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## 從Android SDK型應用程式移轉至fireTV SDK型應用程式 {#migra2}

這個新的fireTV SDK與我們現有的Android SDK和目前的檔案非常類似 **整合我們的Android SDK** <!--http://tve.helpdocsonline.com/android-technical-overview-->可供使用，直到fireTV SDK檔案準備就緒為止。 如果您已有使用Android SDK的Android應用程式，則fireTV應用程式中的fireTV SDK整合應該會相當簡單明瞭。

與現有的Android SDK相比，fireTV SDK上的驗證程式開發將更簡單，因為管理/顯示MVPD登入頁面和擷取AuthN權杖的工作將由AccessEnabler程式庫在內部執行。

## 常見問題集 {#faq}

1. 如何 **SSO** 工作？

   * SSO將可用於所有採用Adobe Primetime驗證的程式設計師應用程式，這些應用程式在同一台Amazon fireTV裝置上使用新的fireTV SDK
   * 在無用戶端REST API上實作的程式設計人員應用程式和在fireTV SDK上實作的應用程式之間使用SSO **不支援**

1. fireTV SSO的MVPD涵蓋範圍為何？

   * **所有MVPD** fireTV SDK將技術上支援由Adobe Primetime整合的驗證SSO。

1. 除了使用新的SDK外，其他 **工作流程變更** 程式設計師應該注意嗎？

   * 程式設計人員需要為fireTV平台實作MVPD選擇器。

1. 驗證是否會有任何變更 **TTL**?

   * 驗證TTL的行為沒有變更。
   * 第一個有效的驗證Token將用於執行SSO，在此情況下，所有將透過SSO驗證的其他應用程式將使用相同的TTL，直到過期為止。 因此，當從一個應用程式導覽至另一個應用程式時，第二個應用程式會共用驗證之第一個應用程式的TTL。

1. 如何 **降級API** 工作？

   * 降級API不需要變更，使用者體驗將與Android裝置上的相同。

1. 如何 **TempPass** 流會受到影響嗎？

   * TempPass流是單螢幕，在任何其他本機裝置上都一樣。

1. 其他Adobe功能是否如以往般運作？

   * 所有Primetime驗證功能在fireTV上和在Android裝置上一樣有效。
