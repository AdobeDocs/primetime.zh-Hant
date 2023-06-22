---
description: 您可以使用由ExpressPlay支援的Primetime DRM Cloud，為TVSDK應用程式實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime存取。
title: 多DRM概述
exl-id: 27614bb6-bfa6-445a-8fb5-a1b8af080bcc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 多DRM工作流程 {#multi-drm-workflows}

您可以使用由ExpressPlay支援的Primetime DRM Cloud，為TVSDK應用程式實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime存取。

## 多DRM概述 {#multi-drm-overview}

Adobe TVSDK支援使用多個DRM方案的DRM保護。 Adobe優惠方案 *Primetime DRM Cloud，由ExpressPlay提供技術支援* 在多個平台上封裝、授權及播放您的視訊內容。

支援的DRM方案包括Adobe *Primetime存取* DRM (AAXS)，以及各種裝置上的原生DRM，包括 [Widevine](https://www.widevine.com) 在Chrome和Android上， [Fairplay](https://developer.apple.com/streaming/fps/) 關於Safari和iOS，以及 [PlayReady](https://www.microsoft.com/playready/) 在Edge和XboxOne上。 請向Adobe代表洽詢，以取得有關這些平台上目前可用哪些DRM方案的資訊，以及未來版本的排程日期。

TVSDK支援任何使用這些通訊協定之授權伺服器所發行的DRM授權。 除了支援多個DRM解決方案外，Adobe還提供 *Primetime DRM Cloud，由ExpressPlay提供技術支援* 作為解決方案，ExpressPlay會針對每個解決方案操作授權伺服器。 這可以簡化您的DRM授權發行需求的設定與維護。

使用 *Primetime DRM Cloud，由ExpressPlay提供技術支援* 若要在TVSDK應用程式中實作DRM需求，您必須先取得 [ExpressPlay.com](https://www.expressplay.com) 帳戶。 ExpressPlay提供數種不同DRM保護方案的授權功能，並提供其他服務，包括封裝和金鑰管理。

您的Adobe代表會先設定您的ExpressPlay帳戶。 然後，您可以設定帳戶並取得 *客戶驗證者* 您將在對ExpressPlay伺服器的授權Token請求中使用的資訊。
