---
description: 若要開始使用由ExpressPlay支援的Primetime DRM Cloud，您需要在Adobe代表的協助下設定AdobeCert和ExpressPlay帳戶。
title: 布建（帳戶等）
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 布建（帳戶等） {#get-provisioned-accounts-etc}

若要開始使用由ExpressPlay支援的Primetime DRM Cloud，您需要在Adobe代表的協助下設定AdobeCert和ExpressPlay帳戶。

1. 請連絡您的Adobe代表，要求您提供使用TVSDK實作多DRM所需的AdobeCert和ExpressPlay帳戶。

   提供您的Adobe代表您將用來作為聯絡視窗的電子郵件地址。 Adobe接著會為您建立兩個帳戶：

   * ***憑證入口網站帳戶*** - ( https://certportal.primetime.adobe.com) ：此 *Adobe存取/Primetime DRM憑證註冊管理團隊* 會傳送電子郵件至您提供的地址。 該電子郵件包含Adobe憑證入口網站的URL，以及Adobe憑證註冊檔案的連結(最新檔案列於此處： [憑證註冊指南](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md))。

   * ***ExpressPlay帳戶*** -Adobe傳送電子郵件給您，其中包含您用來註冊ExpressPlay管理員帳戶的連結。

1. 使用您的Adobe ID登入Adobe憑證入口網站(使用您提供給Adobe代表的相同電子郵件地址)。 如果您還沒有Adobe ID，您可以依照以下步驟快速建立 *取得Adobe ID* 憑證入口網站的連結：

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. 在Adobe憑證入口網站上，請求 *試用版* 憑證。

   對於多DRM試用版，單一試用憑證將涵蓋內容保護的所有方面：包裝、授權和運輸。 您需要提供您自己的 [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) 若要要求憑證：
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe會傳送電子郵件給您，指出您接受或拒絕憑證要求。 您可以在以下網址檢視憑證要求的狀態： *請求歷史記錄* 憑證入口網站上的標籤：
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. 建立您的ExpressPlay管理員帳戶。

   按照提供給您的Adobe連結進入ExpressPlay。 如此將可開啟 *建立帳戶* ExpressPlay頁面。 填寫必填資訊並提交表單。 您將會收到一封來自的電子郵件 `operations@expressplay.com` 包含一週有效的啟用連結。 啟用後，請設定您的ExpressPlay服務：
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   建立服務後，系統會顯示您專屬的「管理員」頁面。 除了一些活動追蹤欄位，您將會看到您的生產和測試 *客戶驗證者* （API金鑰），以及您的生產與測試服務URL：

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. 如果您使用FairPlay，則在Apple開發人員網站上設定使用ExpressPlay時，會涉及其他步驟。 另請參閱 [啟用FairPlay的ExpressPlay服務](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) 以取得指示。
