---
title: 部署Adobe Primetime DRM
description: 部署Adobe Primetime DRM
copied-description: true
exl-id: 64a96d70-502c-48b8-9f43-59f4001a7ab6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 部署Adobe Primetime DRM {#configure-adobe-primetime-drm}

Adobe Primetime DRM SDK的主要優點在於您可將其安裝在任何Java™應用程式伺服器或servlet容器，例如Tomcat。 您也需要JDK™ 1.5或更新版本。 如需軟體需求的詳細資訊，請參閱Primetime DRM SDK平台需求： [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

部署Primetime DRM的高階步驟為：

1. 安裝及設定Primetime DRM SDK。
1. 從Adobe取得數位憑證。
1. 使用SDK建立License Server，或部署Primetime DRM伺服器以使用受保護的串流。
1. 建立內容封裝和原則管理工具，以封裝內容、使用提供的內容準備工具，或授權其中一個AdobeHTTP Dynamic Streaming封裝者。
1. 為您的內容定義使用規則，並建立原則以支援這些規則。
1. 使用封裝和原則管理工具封裝您的內容。
1. 開發視訊應用程式，讓消費者可以使用Flash Player或Adobe AIR檢視您的受保護內容，或使用支援Primetime DRM的成立OVP （線上視訊平台）。
1. 將SWF檔案部署至您的網站以用於Flash Player，或發佈Adobe AIR安裝程式以供下載。

以下各節將展開這些步驟，並參考包含其他資訊的其他檔案。

## 在64位元作業系統上部署{#deploying-on-a-bit-operating-system}

64位元作業系統（例如64位元版的RedHat或Windows）比32位元作業系統提供更好的效能。

## 安裝Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK是以Java封存(JAR)檔案提供。 若要進一步瞭解安裝Primetime DRM，請參閱使用Adobe Primetime DRM SDK保護內容與安全部署准則。

## 實作授權伺服器 {#implement-a-license-server}

使用Adobe Primetime DRM SDK時，您必須建立License Server。 使用Primetime DRM保護內容時，除非授權伺服器向消費者發出授權，否則無法檢視內容。 如果使用以身分為基礎的授權，以密碼為基礎的驗證可確保只有經過授權的消費者才能開啟和檢視內容。

實作License Server時，您必須從Adobe取得必要的數位憑證。 如需請求憑證的詳細說明，請參閱Primetime DRM憑證註冊檔案。

若要進一步瞭解實作License Server及取得數位憑證，請參閱 **使用Adobe Primetime DRM SDK來保護內容。**

## 建立內容封裝和原則管理工具{#create-content-packaging-and-policy-management-tools}

您可以使用Adobe Primetime DRM SDK建立內容封裝和原則管理工具。 原則管理API可讓管理員建立、檢視詳細資料和更新原則。 封裝API會將原則內嵌到視訊檔案中，並使用內容加密金鑰加密檔案。

Primetime DRM SDK包含參考實作( [!DNL AdobePackager.jar])提供內容封裝和原則管理工具的範例( [!DNL AdobePolicyManager.jar])。

若要深入瞭解如何建立內容封裝和原則管理工具，請參閱 **使用Adobe Primetime DRM SDK保護內容。**

## 建立原則和封裝內容 {#create-policies-and-package-content}

您必須使用SDK支援的使用規則，定義並建立原則以支援貴組織的商業模式，然後使用這些原則封裝您的內容。 在封裝期間將原則套用至內容後，無論內容散佈的範圍有多廣，您都可以維持對內容的控制。

Adobe Primetime DRM中的原則支援各種不同的使用規則，包括：

* 指定消費者開始觀看內容後，授權的有效天數。
* 允許授權快取。
* 指定可存取內容的使用者端執行階段和版本(例如，使用者必須具有特定Adobe AIR應用程式或特定版本的Flash Player)。
* 要求消費者在檢視受保護內容之前使用使用者名稱和密碼驗證自己，或允許匿名存取。

若要進一步了解封裝內容，請參閱 *保護內容*. 若要進一步瞭解使用規則及其支援的商業模式，請參閱 *使用規則*.

## 開發視訊播放應用程式 {#develop-applications-for-video-playback}

若要讓消費者能夠存取及檢視內容，請使用Flash Player或Adobe AIR開發視訊播放應用程式。 開發視訊播放應用程式後，您必須將其部署給消費者。 如果您使用Flash Player開發應用程式，請將其託管在您組織的網站上。 如果您使用Adobe® AIR®開發應用程式，請發佈AIR應用程式安裝程式，讓消費者可以下載應用程式並安裝在自己的電腦上。

若要進一步瞭解如何開發自訂視訊播放應用程式以搭配Adobe Primetime DRM使用，請參閱中的「使用視訊」一章 [ActionScript 3.0開發人員指南](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)，則 [Adobe視訊技術中心](https://www.adobe.com/devnet/video/)和Open Source Media Framework。
