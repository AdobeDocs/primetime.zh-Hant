---
description: Gimfire DRM的主要元件包括Java SDK、Flash Player和Adobe AIR客戶端運行時環境。
title: Java SDK、Flash Player和Adobe AIR客戶端
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Adobe PrimetimeDRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

黃金時段DRM作為Java SDK提供，您可以從中建立伺服器實現。 使用SDK，您可以建立適合您組織的業務模型的黃金時段DRM解決方案。

SDK中提供的Java API將在以下子部分中介紹。

## 用於管理設備組域的Java API{#java-apis-for-managing-device-group-domains}

這些API用於允許伺服器處理加入和離開設備組域的客戶端請求。

設備組域是能夠彼此共用許可證的設備的邏輯集合。 為了實現此目的，每台設備必須首先加入/註冊到同一域。 運行在伺服器上的Mighine DRM SDK必須處理設備域加入（註冊）請求以及設備域離開（註銷）請求。 未加入任何域的設備將頒發綁定到該設備的許可證，該許可證不能共用到任何其他設備。

## 用於保護內容的Java API{#java-apis-for-protecting-content}

這些API用於定義權限和準備分發內容。 內容保護API包括：

* 策略管理

   策略管理API用於建立和修改要應用於內容的策略。 可以建立或更新策略，包括獲取/設定所有使用規則以及允許自定義命名空間中的其他參數。

* 內容打包

   內容打包API用於加密內容並從打包的內容中檢索元資料。

## 用於頒發許可證的Java API{#java-apis-for-issuing-licenses}

當客戶端從伺服器請求許可證時，會使用這些API。 SDK支援來自客戶端的以下請求：

* 驗證

   驗證API可用於處理驗證請求和生成驗證令牌。

* 許可證生成和獲取

   許可證生成和獲取API用於為用戶生成許可證。

* 支援Adobe AIR1.5版客戶端和內容

   為了向後相容，SDK具有API來處理來自AIR應用程式的請求，這些應用程式是為與AIR1.5版和更早版本的客戶端和受保護內容一起使用而建立的。

## 參考實現 {#reference-implementation}

SDK包括一個參考實現，一個簡單的Adobe PrimetimeDRM部署，演示如何使用Java API。 該參考實現提供了許可證伺服器、監視資料夾打包器、黃金時段DRM管理器AIR應用程式以及用於基於Java API的內容打包和策略管理的命令行工具。 要瞭解有關黃金時段DRM參考實現的詳細資訊，請參閱保護內容。
