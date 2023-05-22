---
title: 軟體要求
description: 軟體要求
copied-description: true
exl-id: aa2ae6ac-7c2a-4cc3-a3a4-b7f92e478d23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 軟體要求 {#software-requirements}

* Tomcat 6
* JDK 1.8

## 代碼傳遞/包內容{#code-delivery-package-contents}

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

## 獲取個性化伺服器證書{#obtain-individualization-server-certificates}

要使用本地個性化伺服器，必須先獲取兩個數字憑據（證書）:

* *個性化傳輸憑據*  — 由Adobe
* *個性化CA憑據*  — 由Symantec(VeriSign)發佈

要獲取這些證書，請通過Zendesk票證向以下用戶提交請求： [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

請注意，這些憑據是運行Mogfire DRM許可證伺服器所需的憑據之外。
