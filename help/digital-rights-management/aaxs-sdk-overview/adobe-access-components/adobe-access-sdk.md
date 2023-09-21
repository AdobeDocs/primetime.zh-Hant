---
description: Adobe Access的主要元件包含Java SDK、Flash Player和Adobe AIR使用者端執行階段環境。
title: Java SDK、Flash Player和Adobe AIR使用者端
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Adobe存取元件{#adobe-access-components}

Adobe Access的主要元件包含Java SDK、Flash Player和Adobe AIR使用者端執行階段環境。

如需設定SDK的詳細資訊，請參閱以下的「設定SDK」： *使用Adobe存取SDK來保護內容。*

Adobe存取SDK可讓您開發數位版權管理解決方案，該解決方案會與您組織現有的業務基礎建設整合，例如內容管理、帳單和使用者存取控制系統。 Flash Player和Adobe AIR可讓您建立並輕鬆部署應用程式，消費者可透過這些應用程式存取和檢視大型數位內容資料庫。

## Adobe存取SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe存取會以Java SDK的形式提供，此SDK提供建置區塊，供您建立伺服器實作。 使用SDK，您可以建立適合您組織商業模式的Adobe存取解決方案。

以下小節將說明SDK中提供的Java API。

## 用於管理裝置群組網域的Java API {#java-apis-for-managing-device-group-domains}

這些API可讓伺服器處理加入和離開裝置群組網域的使用者端請求。

裝置群組網域是能夠彼此共用授權的裝置的邏輯集合。 為了做到這一點，每個裝置必須首先聯結/註冊到相同的網域。 在伺服器上執行的Adobe存取SDK必須處理裝置網域加入（註冊）請求以及裝置網域離開（取消註冊）請求。 未加入任何網域的裝置將獲得與該裝置繫結的授權，該授權無法與任何其他裝置共用。

## 用於保護內容的Java API {#java-apis-for-protecting-content}

這些API用於定義許可權及準備內容以進行分發。 內容保護API為：

* 原則管理

  原則管理API可用來建立和修改要套用至內容的原則。 您可以建立或更新原則，包括取得/設定所有使用規則，以及允許自訂名稱空間中的其他引數。

* 內容封裝

  內容封裝API用於加密內容，以及從封裝內容中擷取中繼資料。

## 用於發行授權的Java API {#java-apis-for-issuing-licenses}

當使用者端向伺服器要求授權時，就會使用這些API。 SDK支援使用者端的下列要求：

* 驗證

  驗證API可用於處理驗證請求並產生驗證權杖。

* 授權產生與贏取

  授權產生和贏取API用於為使用者產生授權。

* 支援Adobe AIR 1.5版本的使用者端和內容

  為了回溯相容性的目的，SDK有API可處理來自AIR應用程式的請求，這些應用程式是針對AIR 1.5版及舊版使用者端和受保護的內容而建立的。

## 參考實作 {#reference-implementation}

SDK包含參考實作、簡單的Adobe存取部署，示範如何使用Java API。 參考實作提供許可證伺服器、Watched資料夾封裝程式、Adobe存取管理員AIR應用程式，以及根據Java API進行內容封裝和原則管理的命令列工具。 若要進一步瞭解Adobe存取參考實作，請參閱 *保護內容*.

## 適用於受保護串流的Adobe Access Server {#adobe-access-server-for-protected-streaming}

對於使用Adobe存取保護內容的串流使用案例(例如用於AdobeHTTP Dynamic Streaming)，軟體也包括適用於受保護串流的Adobe Access Server 。 此解決方案可輕鬆部署在Tomcat之類的servlet容器上，並可達到高水準的擴充性和效能，以符合最大的內容發佈需求。

## AdobeFlash Player {#adobe-flash-player}

Flash Player是輕量型的瀏覽器外掛程式和執行階段，提供一致且吸引人的使用者體驗、令人驚豔的音訊/視訊播放效果，且觸及範圍廣泛。 Flash Player提供高品質的串流或下載視訊內容播放。 對於內容發佈者，Flash Player提供了自訂內容周圍播放畫面的方法，允許使用橫幅和覆蓋圖透過廣告更深入品牌體驗和獲利。 對於消費者而言，Flash Player能以直觀且美觀的方式檢視視訊內容。

如需Flash Player的詳細資訊，請造訪： [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR是跨作業系統的執行階段，可讓內容製作者透過設計自訂的多媒體應用程式，將現有的網頁投資擴充至案頭。 這套技術以備受肯定的開放式技術為基礎，為企業開發及部署客製化應用程式提供可靠且簡化的方式，值得信賴，提供更安全、更愉快的使用者體驗。 Adobe AIR可讓企業輕鬆整合多媒體，創造更沈浸式互動的使用者體驗。 它可讓開發人員使用熟悉的工具，例如HTML、JavaScript、Flash或Adobe®Flex®軟體，將其豐富的網際網路應用程式獨特組合部署至Windows、Macintosh或Linux。

企業可完全控制使用者介面，且可設計使用者體驗，以反映並強化其品牌。 Adobe AIR內建內容播放支援，並以Adobe Access SDK保護，有助建立自訂的端對端內容發佈鏈。

## 原生iOS和Android應用程式 {#native-ios-and-android-applications}

原生iOS和Android應用程式僅供Adobe Primetime客戶使用，Adobe存取DRM 4.0及更高版本可用於保護行動裝置上的原生(非Flash)應用程式中使用的視訊。 為了讓應用程式使用此受保護內容，必須使用Adobe Primetime使用者端程式庫實作。

如需Adobe Primetime的詳細資訊，請造訪： [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
