---
description: 您可以使用由ExpressPlay支援的Primetime DRM Cloud，為TVSDK應用程式實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady以及Adobe的Primetime存取。
title: 多DRM概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 多DRM工作流程 {#multi-drm-workflows}

您可以使用由ExpressPlay支援的Primetime DRM Cloud，為TVSDK應用程式實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady以及Adobe的Primetime存取。

## 多DRM概述 {#multi-drm-overview}

Adobe TVSDK支援使用多個DRM配置的DRM保護。 Adobe優惠方案 *Primetime DRM Cloud，由ExpressPlay提供技術支援* 在多個平台上封裝、授權及播放視訊內容。

支援的DRM配置包括Adobe *Primetime存取* DRM (AAXS)，以及各種裝置上的原生DRM，包括 [Widevine](https://www.widevine.com) 在Chrome和Android上， [FairPlay](https://developer.apple.com/streaming/fps/) 關於Safari和iOS，以及 [PlayReady](https://www.microsoft.com/playready/) 在Edge和XboxOne。 請洽詢Adobe代表，瞭解目前在這些平台上可以使用哪些DRM方案，以及未來版本的預定日期。

TVSDK支援任何使用這些通訊協定之授權伺服器所發行的DRM授權。 除了支援多個DRM解決方案外，Adobe還提供 *Primetime DRM Cloud，由ExpressPlay提供技術支援* 作為解決方案，ExpressPlay會針對每個解決方案操作授權伺服器。 這可以簡化您的DRM授權發行需求的設定與維護。

使用 *Primetime DRM Cloud，由ExpressPlay提供技術支援* 若要在TVSDK應用程式中實作DRM需求，您必須先取得 [ExpressPlay.com](https://www.expressplay.com) 帳戶。 ExpressPlay提供多種不同DRM保護方案的授權功能，並提供其他服務，包括封裝和金鑰管理。

您的Adobe代表一開始會設定您的ExpressPlay帳戶。 然後，您可以設定帳戶並取得 *客戶驗證者* 您將在對ExpressPlay伺服器的授權Token要求中使用的權杖。
