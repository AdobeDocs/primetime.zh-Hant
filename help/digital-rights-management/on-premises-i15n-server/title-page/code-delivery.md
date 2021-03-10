---
title: 程式碼傳送／封裝內容
description: 程式碼傳送／封裝內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 程式碼傳送／封裝內容{#code-delivery-package-contents}

Adobe PrimetimeDRM On Promiess Personalization Server軟體包包含以下內容：

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

