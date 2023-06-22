---
title: 程式碼傳送/封裝內容
description: 程式碼傳送/封裝內容
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 程式碼傳送/封裝內容{#code-delivery-package-contents}

Adobe Primetime DRM On Premises Individualization Server套件包含下列專案：

* [!DNL flashaccess.war]  — 個人化伺服器
* [!DNL flashaccess-kgs.war]  — 選購的金鑰產生伺服器
* [!DNL /shared]  — 包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties]  — 屬性檔案範例

* [!DNL thirdparty/]  — 包含Crypto-J支援作為原生程式庫：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar]  — 加密伺服器認證密碼的公用程式
* [!DNL ROOT]  — 包含 [!DNL crossdomain.xml] 檔案

* ECI快取檔案 — 預先下載
* [!DNL addIndivCert.py]  — 用於更新授權伺服器的信任根以支援內部部署個人化的指令碼
* [!DNL CreateMetadata.jar]  — 建立內部部署DRM中繼資料的公用程式
* [!DNL client_sample/]  — 包含使用者端程式碼片段的資料夾
* 發行說明 — 說明檔案在最後一刻的任何新增

