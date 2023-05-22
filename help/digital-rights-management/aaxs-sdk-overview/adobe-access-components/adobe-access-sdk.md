---
description: Adobe訪問的主要元件包括Java SDK、Flash Player和Adobe AIR客戶端運行時環境。
title: Java SDK、Flash Player和Adobe AIR客戶端
exl-id: 2df4da13-8df9-442b-8638-317c41d62fbe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Adobe訪問元件{#adobe-access-components}

Adobe訪問的主要元件包括Java SDK、Flash Player和Adobe AIR客戶端運行時環境。

有關設定SDK的詳細資訊，請參閱中的設定SDK *使用Adobe訪問SDK保護內容。*

Adobe訪問SDK允許您開發一個數字權限管理解決方案，該解決方案與您公司的現有業務基礎架構（如內容管理、計費和用戶訪問控制系統）整合。 Flash Player和Adobe AIR讓您能夠建立並輕鬆部署應用程式，通過這些應用程式，消費者可以訪問和查看大型數字內容庫。

## Adobe訪問SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe訪問作為Java SDK提供，您可以從中建立伺服器實現。 使用SDK，您可以建立適合您組織的業務模型的Adobe訪問解決方案。

SDK中提供的Java API將在以下子部分中介紹。

## 用於管理設備組域的Java API {#java-apis-for-managing-device-group-domains}

這些API用於允許伺服器處理加入和離開設備組域的客戶端請求。

設備組域是能夠彼此共用許可證的設備的邏輯集合。 為了實現此目的，每台設備必須首先加入/註冊到同一域。 Adobe訪問SDK（在伺服器上運行）必須處理設備域加入（註冊）請求以及設備域離開（註銷）請求。 未加入任何域的設備將頒發綁定到該設備的許可證，該許可證不能共用到任何其他設備。

## 用於保護內容的Java API {#java-apis-for-protecting-content}

這些API用於定義權限和準備分發內容。 內容保護API包括：

* 策略管理

   策略管理API用於建立和修改要應用於內容的策略。 可以建立或更新策略，包括獲取/設定所有使用規則以及允許自定義命名空間中的其他參數。

* 內容打包

   內容打包API用於加密內容並從打包的內容中檢索元資料。

## 用於頒發許可證的Java API {#java-apis-for-issuing-licenses}

當客戶端從伺服器請求許可證時，會使用這些API。 SDK支援來自客戶端的以下請求：

* 驗證

   驗證API可用於處理驗證請求和生成驗證令牌。

* 許可證生成和獲取

   許可證生成和獲取API用於為用戶生成許可證。

* 支援Adobe AIR1.5版客戶端和內容

   為了向後相容，SDK具有API來處理來自AIR應用程式的請求，這些應用程式是為與AIR1.5版和更早版本的客戶端和受保護內容一起使用而建立的。

## 參考實現 {#reference-implementation}

SDK包括一個引用實現，一個簡單的Adobe訪問部署，演示如何使用Java API。 該參考實現提供了許可證伺服器、受監視資料夾打包器、Adobe訪問管理器AIR應用程式以及用於基於Java API的內容打包和策略管理的命令行工具。 要瞭解有關Adobe訪問參考實現的詳細資訊，請參閱 *保護內容*。

## Adobe Access Server用於受保護的流式處理 {#adobe-access-server-for-protected-streaming}

對於使用Adobe訪問保護內容的流式使用情形，如AdobeHTTP Dynamic Streaming，軟體還包括「受保護流式」的Adobe Access Server。 此解決方案可以輕鬆地部署在Servlet容器（如Tomcat）上，並可實現高級別的可擴充性和效能以滿足最大的內容分發需求。

## AdobeFlash Player {#adobe-flash-player}

Flash Player是一種輕量級的瀏覽器插件和運行時，可提供一致且引人入勝的用戶體驗、令人驚嘆的音頻/視頻回放和普及的訪問。 Flash Player提供流式或下載的視頻內容的高質量回放。 對於內容發佈者，Flash Player提供了定制圍繞內容的播放螢幕的方法，允許通過使用橫幅和覆蓋的廣告來加深品牌體驗和賺錢。 對於消費者來說，Flash Player提供了一種直觀、直觀的視頻內容觀看方式。

有關Flash Player的詳細資訊，請訪問： [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR是一個跨作業系統運行時，它允許內容製作商通過設計定製的多媒體應用程式將他們在Web上的現有投資擴展到案頭。 它構建在經驗證的開放技術之上，為企業開發和部署可信賴的定製應用程式提供了可靠、簡化的方法，以提供更安全、更愉快的用戶體驗。 Adobe AIR公司使企業能夠輕鬆整合富媒體，創造更身臨其境的互動用戶體驗。 它使開發人員能夠使用HTML、JavaScript、Flash或Adobe®Flex®軟體等熟悉的工具，將富Internet應用程式的獨特組合部署到Windows、Macintosh或Linux。

企業對用戶介面有完全的控制，可以設計用戶體驗來反映和強化其品牌。 通過內置支援播放使用AdobeAccess SDK保護的內容，Adobe AIR幫助建立自定義的端到端內容分發鏈。

有關Adobe AIR的更多資訊，請訪問： [www.adobe.com/go/air](https://www.adobe.com/go/air)

## 本地iOS和Android應用程式 {#native-ios-and-android-applications}

本機iOS和Android應用程式僅供Adobe Primetime客戶使用，Adobe訪問DRM 4.0及更高版本可用於保護移動設備上本機(非Flash)應用程式內使用的視頻。 為了使應用程式使用此受保護的內容，必須使用Adobe Primetime客戶端庫來實現。

有關Adobe Primetime的更多資訊，請訪問： [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
