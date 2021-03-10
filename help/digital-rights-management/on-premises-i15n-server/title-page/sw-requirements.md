---
title: 軟體需求
description: 軟體需求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 軟體要求{#software-requirements}

* Tomcat 6
* JDK 1.8

## 程式碼傳送／封裝內容{#code-delivery-package-contents}

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

## 取得個人化伺服器憑證{#obtain-individualization-server-certificates}

要使用內部個人化伺服器，您必須首先獲得兩個數字證書（證書）:

* *個人化運輸憑證* -由Adobe核發
* *個性化CA憑證* -由Symantec(VeriSign)頒發

若要取得這些憑證，請透過Zendesk票證提交要求至：[https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

請注意，這些認證是除了Primetime DRM授權伺服器作業所需的認證之外。