---
title: 代碼傳遞/包內容
description: 代碼傳遞/包內容
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 代碼傳遞/包內容{#code-delivery-package-contents}

Adobe PrimetimeDRM On Premises個性化伺服器包包含以下內容：

* [!DNL flashaccess.war]  — 個性化伺服器
* [!DNL flashaccess-kgs.war]  — 可選密鑰生成伺服器
* [!DNL /shared]  — 包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties]  — 示例屬性檔案

* [!DNL thirdparty/]  — 將Crypto-J支援作為本機庫包括：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar]  — 用於加密伺服器憑據密碼的實用程式
* [!DNL ROOT]  — 包含 [!DNL crossdomain.xml] 檔案

* ECI快取檔案 — 預下載
* [!DNL addIndivCert.py]  — 用於更新許可證伺服器的信任根以支援本地個性化的指令碼
* [!DNL CreateMetadata.jar]  — 用於建立本地DRM元資料的實用程式
* [!DNL client_sample/]  — 包含客戶端代碼段的資料夾
* 發行說明 — 在文檔的最後一刻添加內容

