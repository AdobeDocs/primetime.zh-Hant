---
title: 部署Adobe訪問
description: 部署Adobe訪問
copied-description: true
exl-id: bebf02d5-897e-4007-8c5c-1c91186fdc51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# 部署Adobe訪問 {#deploy-adobe-access}

AdobeAccess SDK的一個關鍵優勢是，您可以在任何Java™應用程式伺服器或Servlet容器（如Tomcat）上安裝它。 您還需要JDK™ 1.5或更高版本。 有關軟體要求的詳細資訊，請參閱Adobe訪問SDK平台要求： [:https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/)。

部署Adobe訪問的高級步驟包括：

1. 安裝和配置Adobe訪問SDK。
1. 從Adobe獲取數字證書。
1. 使用SDK建立許可證伺服器，或部署Adobe Access Server以進行受保護的流。
1. 建立內容打包和策略管理工具以打包內容、使用提供的內容準備工具或許可AdobeHTTP Dynamic Streaming打包器之一。
1. 定義內容的使用規則，並建立支援這些規則的策略。
1. 使用打包和策略管理工具打包您的內容。
1. 開發視頻應用程式，讓消費者可以使用Flash Player或Adobe AIR查看受保護的內容，或使用支援Adobe訪問的已建立的OVP（線上視頻平台）。
1. 將SWF檔案部署為與Flash Player一起使用到您的網站，或將Adobe AIR安裝程式發佈以供下載。

這些步驟在以下各節中展開，其中引用了包含其他資訊的其他文檔。

## 部署在64位作業系統上 {#deploying-on-a-bit-operating-system}

64位作業系統（如64位版本的RedHat或Windows）比32位作業系統提供的效能要好得多。

## 安裝Adobe訪問SDK {#install-adobe-access-sdk}

Adobe訪問SDK作為Java存檔(JAR)檔案提供。 要瞭解有關安裝Adobe訪問的詳細資訊，請參見 *使用Adobe訪問SDK保護內容*&#x200B;和&#x200B;*安全部署准則*。

## 實施許可證伺服器 {#implement-a-license-server}

使用Adobe訪問SDK，必須建立許可證伺服器。 使用Adobe訪問保護內容時，只有在許可證伺服器向使用者頒發許可證後，才能查看內容。 如果使用基於身份的許可，則基於密碼的身份驗證可確保只有經過授權的消費者才能開啟和查看內容。

在實施許可證伺服器時，必須從Adobe獲取必要的數字證書。 有關請求證書的詳細說明，請參閱Adobe訪問證書註冊文檔。

要瞭解有關實施許可證伺服器和獲取數字證書的詳細資訊，請參閱*使用Adobe訪問SDK保護內容。*

## 建立內容打包和策略管理工具 {#create-content-packaging-and-policy-management-tools}

使用Adobe訪問SDK，可以建立內容打包和策略管理工具。 策略管理API允許管理員建立、查看策略的詳細資訊和更新策略。 打包API將策略嵌入到FLV或F4V檔案中，並使用內容加密密鑰對檔案進行加密。

Adobe訪問SDK包括引用實現( [!DNL AdobePackager.jar])提供內容打包和策略管理工具的示例( [!DNL AdobePolicyManager.jar])。

要瞭解有關建立內容打包和策略管理工具的詳細資訊，請參見 *使用Adobe訪問SDK保護內容*。

## 建立策略和包內容 {#create-policies-and-package-content}

使用SDK支援的使用規則，您必須定義並建立支援組織業務模型的策略，然後使用這些策略打包您的內容。 一旦策略在打包期間應用到內容，您就可以保持對內容的控制，無論內容的分發範圍有多廣。

Adobe訪問中的策略支援多種不同的使用規則，包括：

* 指定一旦用戶開始監視內容，許可證有效的天數。
* 允許許可證快取。
* 指定可訪問內容的客戶端運行時和版本(例如，用戶必須具有特定的Adobe AIR應用程式或特定版本的Flash Player)。
* 要求消費者在查看受保護的內容或允許匿名訪問之前使用用戶名和密碼進行身份驗證。

要瞭解有關打包內容的詳細資訊，請參閱 *保護內容*。 要瞭解有關使用規則及其支援的業務模型的更多資訊，請參見 *使用規則*。

## 開發視頻回放應用程式 {#develop-applications-for-video-playback}

要使消費者能夠訪問和查看內容，請使用Flash Player或Adobe AIR開發視頻播放應用程式。 開發視頻播放應用程式後，必須將其部署到消費者。 如果您正在使用Flash Player開發應用程式，請將其托管在您組織的網站上。 如果您正在使用Adobe® AIR®開發應用程式，請發佈AIR應用程式安裝程式，以便消費者可以在其電腦上下載並安裝應用程式。

要瞭解有關開發自定義視頻播放應用程式以與Adobe訪問一起使用的詳細資訊，請參閱中的「使用視頻」一章 [ActionScript3.0開發人員指南](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*、* [Adobe視頻技術中心](https://www.adobe.com/devnet/video/)和Open Source Media Framework。
