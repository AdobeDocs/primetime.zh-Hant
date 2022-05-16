---
description: 要開始使用由ExpressPlay支援的Mighide DRM雲，您需要在Adobe代表的幫助下設定Adobe證書和ExpressPlay帳戶。
title: 獲取預配（帳戶等）
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 獲取預配（帳戶等） {#get-provisioned-accounts-etc}

要開始使用由ExpressPlay支援的Mighide DRM雲，您需要在Adobe代表的幫助下設定Adobe證書和ExpressPlay帳戶。

1. 與Adobe代表聯繫，並請求您使用TVSDK實現多DRM所需的Adobe證書和ExpressPlay帳戶。

   向Adobe代表提供您將用作聯繫人的電子郵件地址。 Adobe，然後為您建立兩個帳戶：

   * ***證書門戶帳戶*** -(https://certportal.primetime.adobe.com):的 *Adobe訪問/黃金時段DRM證書註冊管理團隊* 向您提供的地址發送電子郵件。 該電子郵件包含Adobe證書門戶的URL，以及指向Adobe證書註冊文檔的連結(最新文檔在此處： [證書註冊指南](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md))。

   * ***ExpressPlay帳戶*** -Adobe向您發送一封電子郵件，其中包含您用於註冊ExpressPlay管理帳戶的連結。

1. 使用Adobe ID登錄Adobe證書門戶(使用您向Adobe代表提供的相同電子郵件地址)。 如果您尚未擁有Adobe ID，則可以通過以下方式快速建立 *找個Adobe ID* 從證書門戶連結：

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. 在Adobe證書門戶上，請求 *審判* 證書。

   對於Multi-DRM試用，單個試用證書將涵蓋內容保護的所有方面：包裝、許可和運輸。 你需要自己提供 [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) 請求證書：
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe會向您發送一封電子郵件，指示您接受或拒絕證書請求。 您可以在 *請求歷史記錄* 頁籤：
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. 建立ExpressPlay管理帳戶。

   按照該Adobe提供給您的ExpressPlay的連結操作。 開啟 *建立帳戶* 頁面。 填寫所需資訊並提交表單。 您將收到來自 `operations@expressplay.com` 包含一週有效的激活連結。 激活後，請設定ExpressPlay服務：
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   建立服務後，將顯示您自己的「管理」頁。 除了某些活動跟蹤欄位外，您還將看到您的生產和Test *客戶身份驗證器* （API鍵），以及您的生產和Test服務URL:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. 如果您使用FairPlay，則需要執行其他步驟(在Apple開發人員網站上)來設定ExpressPlay。 請參閱 [為FairPlay啟用ExpressPlay服務](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) 的雙曲餘切值。
