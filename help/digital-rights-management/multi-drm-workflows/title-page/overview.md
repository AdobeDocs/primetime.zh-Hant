---
description: 您可以使用Primetime DRM Cloud為TVSDK應用程式（由ExpressPlay提供支援）實作多個DRM解決方案。 DRM解決方案包括蘋果的FairPlay、谷歌的Widevine、微軟的PlayReady和Primetime Access fromAdobe。
title: 多DRM概觀
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 多DRM工作流程{#multi-drm-workflows}

您可以使用Primetime DRM Cloud為TVSDK應用程式（由ExpressPlay提供支援）實作多個DRM解決方案。 DRM解決方案包括蘋果的FairPlay、谷歌的Widevine、微軟的PlayReady和Primetime Access fromAdobe。

## 多DRM概觀{#multi-drm-overview}

AdobeTVSDK支援使用多個DRM方案的DRM保護。 Adobe提供&#x200B;*Primetime DRM Cloud，採用ExpressPlay*，以在多種平台上封裝、授權和播放您的視訊內容。

支援的DRM方案包括Adobe的&#x200B;*黃金時段存取* DRM(AAXS)，以及各種裝置上的原生DRM，包括Chrome和Android上的[Widevine](https://www.widevine.com)、Safari和iOS上的[FarPlay](https://developer.apple.com/streaming/fps/)和[在Edge和XboxOne上播放Ready](https://www.microsoft.com/playready/)。 請洽詢Adobe代表，以取得有關這些平台目前有哪些DRM方案可用的資訊，以及未來發行的排程日期。

TVSDK支援任何使用這些通訊協定的授權伺服器所核發的DRM授權。 除了支援多種DRM解決方案外，Adobe還提供&#x200B;*Primetime DRM Cloud，由ExpressPlay*&#x200B;提供支援，作為ExpressPlay為每個解決方案運作授權伺服器的解決方案。 這可以簡化DRM授權發行需求的設定與維護。

若要使用&#x200B;*Primetime DRM Cloud（採用ExpressPlay*&#x200B;的架構）在TVSDK應用程式中實作DRM需求，您必須先取得[ExpressPlay.com](https://www.expressplay.com)帳戶。 ExpressPlay為幾種不同的DRM保護方案提供許可功能，還提供包裝和密鑰管理等其他服務。

您的Adobe代表會先設定您的ExpressPlay帳戶。 然後，您可以設定帳戶並取得&#x200B;*客戶驗證者*，以便用於ExpressPlay伺服器的授權Token請求。