---
description: Adobe存取的主要元件包括Java SDK，以及Flash Player和Adobe AIR用戶端執行時期環境。
title: Java SDK、Flash Player和Adobe AIR用戶端
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Adobe訪問元件{#adobe-access-components}

Adobe存取的主要元件包括Java SDK，以及Flash Player和Adobe AIR用戶端執行時期環境。

如需設定SDK的詳細資訊，請參閱&#x200B;*使用Adobe存取SDK保護內容中的設定SDK。*

Adobe存取SDK可讓您開發數位版權管理解決方案，以整合貴組織現有的商業基礎架構，例如內容管理、帳單和使用者存取控制系統。 Flash Player和Adobe AIR可讓您建立並輕鬆部署應用程式，讓消費者透過這些應用程式存取和檢視大型數位內容資料庫。

## Adobe存取SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe存取是以Java SDK形式提供，提供您可從中建立伺服器實作的建立區塊。 使用SDK，您可以建立適合您組織業務模式的Adobe存取解決方案。

SDK中提供的Java API將於下列子節中說明。

## 用於管理設備組域{#java-apis-for-managing-device-group-domains}的Java API

這些API可讓伺服器處理用戶端要求加入和離開裝置群組網域。

裝置群組網域是可彼此共用授權的裝置的邏輯集合。 為了達到此目的，每台設備必須先加入／註冊到同一個域。 Adobe存取SDK（在伺服器上執行）必須處理裝置網域加入（註冊）請求，以及裝置網域離開（取消註冊）請求。 未加入任何網域的裝置將會取得系結至該裝置的授權，無法共用給任何其他裝置。

## 用於保護內容{#java-apis-for-protecting-content}的Java API

這些API可用來定義權限並準備內容以供散發。 內容保護API包括：

* 策略管理

   策略管理API用於建立和修改要應用於內容的策略。 可以建立或更新策略，包括獲取／設定所有使用規則以及允許自定義命名空間中的其他參數。

* 內容封裝

   內容封裝API用於加密內容並從封裝內容擷取中繼資料。

## 用於發行{#java-apis-for-issuing-licenses}授權的Java API

當用戶端向伺服器要求授權時，會使用這些API。 SDK支援來自用戶端的下列要求：

* 驗證

   驗證API可用來處理驗證請求並產生驗證Token。

* 授權製作與取得

   授權產生與贏取API可用來為使用者產生授權。

* 支援Adobe AIR1.5版用戶端和內容

   為了向後相容，SDK有API可處理針對AIR 1.5版及舊版用戶端所建立之AIR應用程式的要求，以及受保護的內容。

## 參考實施{#reference-implementation}

SDK包含參考實作、簡單的Adobe存取部署，示範如何使用Java API。 參考實作提供授權伺服器、Watched Folder Packager、Adobe存取管理器AIR應用程式，以及以Java API為基礎的內容封裝與原則管理命令列工具。 要瞭解有關Adobe訪問參考實施的詳細資訊，請參閱&#x200B;*保護內容*。

## Adobe Access Server保護串流{#adobe-access-server-for-protected-streaming}

對於使用Adobe存取保護內容(例如AdobeHTTP Dynamic Streaming)的串流使用案例，本軟體也包含「受保護串流」的Adobe Access Server。 此解決方案可輕鬆部署在Servlet容器（例如Tomcat）上，並可達到高階的可擴充性與效能，以符合最大的內容散發需求。

## AdobeFlash Player{#adobe-flash-player}

Flash Player是輕量型的瀏覽器外掛程式和執行時期，可提供一貫而引人入勝的使用者體驗、令人驚艷的音訊／視訊播放，以及廣泛的觸及面。 Flash Player提供高品質的串流或下載視訊內容播放。 對於內容發佈者，Flash Player提供自訂內容周圍播放畫面的方式，讓您透過使用橫幅和覆蓋的廣告獲得更深入的品牌體驗和獲利。 對於消費者而言，Flash Player提供直覺式且視覺上吸引人的視訊內容檢視方式。

有關Flash Player的更多資訊，請造訪：[www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR{#adobe-air}

Adobe AIR是跨作業系統執行時期，可讓內容製作者透過設計自訂的多媒體應用程式，將其現有的網路投資擴充至案頭。 它以證實可行的開放技術為基礎，為企業提供可靠、簡化的方式來開發和部署可信賴的自訂應用程式，以提供更安全、更愉快的使用者體驗。 Adobe AIR公司可讓企業輕鬆整合多媒體，以建立更身歷其境、更具互動性的使用者體驗。 它可讓開發人員使用熟悉的工具，例如HTML、JavaScript、Flash或Adobe®Flex®軟體，將其獨特的Rich Internet Applications組合部署至Windows、Macintosh或Linux。

企業可完全控制使用者介面，並可設計使用者體驗來反映和強化其品牌。 Adobe AIR支援播放使用Adobe存取SDK保護的內容，協助建立自訂的端對端內容發佈鏈。

有關Adobe AIR的更多資訊，請造訪：[www.adobe.com/go/air](https://www.adobe.com/go/air)

## 原生iOS和Android應用程式{#native-ios-and-android-applications}

原生iOS和Android應用程式僅提供給Adobe Primetime客戶，Adobe存取DRM 4.0和更新版本可用來保護在行動裝置上原生(非Flash)應用程式內耗用的視訊。 為使應用程式使用此受保護的內容，必須使用Adobe Primetime用戶端程式庫來建置。

有關Adobe Primetime的更多資訊，請造訪：[https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)