---
title: 部署Adobe PrimetimeDRM
description: 部署Adobe PrimetimeDRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# 部署Adobe PrimetimeDRM {#configure-adobe-primetime-drm}

Adobe PrimetimeDRM SDK的主要優點是，您可將它安裝在任何Java™應用程式伺服器或servlet容器（例如Tomcat）上。 您還需要JDK™ 1.5或更高版本。 如需軟體需求的詳細資訊，請參閱Primetime DRM SDK平台需求：[https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/)。

部署Primetime DRM的高階步驟包括：

1. 安裝及設定Primetime DRM SDK。
1. 從Adobe取得數位憑證。
1. 使用SDK建立授權伺服器，或部署Primetime DRM伺服器以進行受保護的串流。
1. 建立內容封裝和原則管理工具以封裝內容、使用所提供的內容準備工具，或授權其中一個AdobeHTTP Dynamic Streaming封裝器。
1. 定義內容的使用規則，並建立支援這些規則的原則。
1. 使用封裝與原則管理工具封裝您的內容。
1. 開發視訊應用程式，讓消費者可使用Flash Player或Adobe AIR來檢視您的受保護內容，或使用支援Primetime DRM的現有OVP（線上視訊平台）。
1. 部署SWF檔案以搭配Flash Player至您的網站，或張貼Adobe AIR安裝程式以進行下載。

這些步驟在以下幾節中展開，其中引用了包含其他資訊的其他文檔。

## 部署在64位元作業系統{#deploying-on-a-bit-operating-system}

64位元作業系統（例如64位元版本的RedHat或Windows）提供比32位元作業系統更好的效能。

## 安裝Adobe PrimetimeDRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK以Java封存(JAR)檔提供。 如需有關安裝Primetime DRM的詳細資訊，請參閱「使用Adobe PrimetimeDRM SDK保護內容與安全部署准則」。

## 實施許可證伺服器{#implement-a-license-server}

使用Adobe PrimetimeDRM SDK，您必須建立授權伺服器。 當內容使用Primetime DRM受到保護時，除非授權伺服器向消費者核發授權，否則無法檢視內容。 如果使用以身分為基礎的授權，則以密碼為基礎的驗證可確保只有經過授權的消費者才能開啟和檢視內容。

實作授權伺服器時，您必須從Adobe取得必要的數位憑證。 請參閱Primetime DRM憑證註冊檔案，以取得有關申請憑證的詳細指示。

若要進一步瞭解實作授權伺服器及取得數位憑證，請參閱&#x200B;**使用Adobe PrimetimeDRM SDK保護內容。**

## 建立內容封裝和原則管理工具{#create-content-packaging-and-policy-management-tools}

使用Adobe PrimetimeDRM SDK，您可以建立內容封裝和政策管理工具。 原則管理API可讓管理員建立、檢視政策的詳細資訊，以及更新政策。 封裝API會將原則內嵌在視訊檔案中，並使用內容加密金鑰加密檔案。

Primetime DRM SDK包含參考實作([!DNL AdobePackager.jar])，提供內容封裝與原則管理工具([!DNL AdobePolicyManager.jar])的範例。

若要進一步瞭解如何建立內容封裝和原則管理工具，請參閱&#x200B;**使用Adobe PrimetimeDRM SDK保護內容。**

## 建立策略和包內容{#create-policies-and-package-content}

使用SDK支援的使用規則，您必須定義並建立支援您組織商業模型的原則，然後使用這些原則封裝您的內容。 一旦在封裝期間將原則套用至內容，您就可以控制內容，不論內容的散布範圍有多廣。

Adobe PrimetimeDRM中的政策支援多種不同的使用規則，包括：

* 指定消費者開始觀看內容後，授權的有效天數。
* 允許授權快取。
* 指定可存取內容的用戶端執行時期和版本(例如，使用者必須擁有特定的Adobe AIR應用程式或特定版本的Flash Player)。
* 要求消費者在檢視受保護的內容或允許匿名存取之前，先使用使用者名稱和密碼來驗證自己。

若要進一步瞭解封裝內容，請參閱&#x200B;*保護內容*。 如需進一步瞭解使用規則及其支援的商業模型，請參閱&#x200B;*使用規則*。

## 開發視訊播放應用程式{#develop-applications-for-video-playback}

若要讓消費者存取和檢視內容，請使用Flash Player或Adobe AIR來開發視訊播放應用程式。 開發視訊播放應用程式後，您必須將它部署給消費者。 如果您使用Flash Player來開發應用程式，請將它代管在組織的網站上。 如果您使用Adobe® AIR®開發應用程式，請張貼AIR應用程式安裝程式，讓消費者可下載並安裝應用程式至其電腦。

若要進一步瞭解開發自訂視訊播放應用程式以搭配Adobe PrimetimeDRM使用，請參閱[ActionScript3.0開發人員指南](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)、[Adobe視訊技術中心](https://www.adobe.com/devnet/video/)和Open Source Media Framework中的「使用視訊」一章。