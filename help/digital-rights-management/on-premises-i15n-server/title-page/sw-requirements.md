---
title: 軟體需求
description: 軟體需求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 軟體需求 {#software-requirements}

* Tomcat 6
* JDK 1.8

## 程式碼傳送/封裝內容{#code-delivery-package-contents}

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
* 發行說明 — 說明檔案在最後一分鐘的任何新增

## 取得個人化伺服器憑證{#obtain-individualization-server-certificates}

若要使用On Premises Individualization Server，您必須先取得兩個數位憑證（憑證）：

* *個人化傳輸認證*  — 由Adobe簽發
* *個人化CA認證*  — 由Symantec (VeriSign)簽發

若要取得這些憑證，請透過Zendesk票證將請求提交至： [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

請注意，這些認證是操作Primetime DRM授權伺服器所需的認證以外的認證。
