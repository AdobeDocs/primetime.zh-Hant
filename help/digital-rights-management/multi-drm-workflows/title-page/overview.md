---
description: 您可以使用Primetime DRM Cloud為TVSDK應用程式（由ExpressPlay提供支援）實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime Access。
seo-description: 您可以使用Primetime DRM Cloud為TVSDK應用程式（由ExpressPlay提供支援）實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime Access。
seo-title: 多DRM概觀
title: 多DRM概觀
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 多DRM工作流程 {#multi-drm-workflows}

您可以使用Primetime DRM Cloud為TVSDK應用程式（由ExpressPlay提供支援）實作多個DRM解決方案。 DRM解決方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime Access。

## 多DRM概觀 {#multi-drm-overview}

Adobe TVSDK支援使用多種DRM方案的DRM保護。 Adobe提供 *Primetime DRM Cloud，採用ExpressPlay* ，可在多種平台上封裝、授權和播放您的視訊內容。

支援的DRM方案包括Adobe在 *Primetime Access* DRM(AS)，以及各種裝置上的原生DRM，包括 [Widevine](https://www.widevine.com) on Chrome和Android、 [](https://developer.apple.com/streaming/fps/)[](https://www.microsoft.com/playready/) FairPlay Play On Safari和i OS，以及Adobe Play Redy Edge和Xbox One。 請洽詢Adobe代表，以取得有關這些平台目前有哪些DRM方案可用的資訊，以及未來發行的排程日期。

TVSDK支援任何使用這些通訊協定的授權伺服器所核發的DRM授權。 除了支援多種DRM解決方案外，Adobe還提供 ** Primetime DRM Cloud，由ExpressPlay提供支援，做為ExpressPlay為各解決方案運作授權伺服器的解決方案。 這可以簡化DRM授權發行需求的設定與維護。

若要使 *用Primetime DRM Cloud(採用ExpressPlay* )，在TVSDK應用程式中實作您的DRM需求，您必須先取得 [](https://www.expressplay.com) ExpressPlay.com帳戶。 ExpressPlay為幾種不同的DRM保護方案提供許可功能，還提供包裝和密鑰管理等其他服務。

您的Adobe代表會先設定您的ExpressPlay帳戶。 然後，您可以設定帳戶並取得 *客戶驗證器* ，以便在ExpressPlay伺服器的授權Token請求中使用。