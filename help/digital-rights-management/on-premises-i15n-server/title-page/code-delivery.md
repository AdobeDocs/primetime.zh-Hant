---
seo-title: 程式碼傳送／封裝內容
title: 程式碼傳送／封裝內容
uuid: 13de2fd4-9079-496c-a087-25176c118864
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 程式碼傳送／封裝內容{#code-delivery-package-contents}

Adobe Primetime DRM On Promiess Indificialization Server套件包含下列內容：

* [!DNL flashaccess.war] -個人化伺服器
* [!DNL flashaccess-kgs.war] -可選的密鑰生成伺服器
* [!DNL /shared] -包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] -示例屬性檔案

* [!DNL thirdparty/] -將Crypto-J支援作為本地庫：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] -用於加密伺服器憑據密碼的實用程式
* [!DNL ROOT] -包含文 [!DNL crossdomain.xml] 件

* ECI快取檔案——預先下載
* [!DNL addIndivCert.py] -用於更新許可證伺服器的信任根以支援內部個性化的指令碼
* [!DNL CreateMetadata.jar] -用於建立內部DRM元資料的實用程式
* [!DNL client_sample/] -包含用戶端程式碼片段的資料夾
* 發行說明——針對檔案的最後一刻新增內容

