---
description: 您可以使用ExpressPlay支援的Mogfise DRM雲為TVSDK應用實現多個DRM解決方案。 DRM解決方案包括Apple的FairPlay,Google的Widevine,Microsoft的PlayReady，以及來自Adobe的黃金時段訪問。
title: 多DRM概述
exl-id: 27614bb6-bfa6-445a-8fb5-a1b8af080bcc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 多DRM工作流 {#multi-drm-workflows}

您可以使用ExpressPlay支援的Mogfise DRM雲為TVSDK應用實現多個DRM解決方案。 DRM解決方案包括Apple的FairPlay,Google的Widevine,Microsoft的PlayReady，以及來自Adobe的黃金時段訪問。

## 多DRM概述 {#multi-drm-overview}

AdobeTVSDK支援使用多個DRM方案的DRM保護。 Adobe *由ExpressPlay提供支援的黃金時段DRM雲* 在多個平台上提供視頻內容的打包、許可和回放。

支援的DRM方案包括Adobe *黃金時段訪問* DRM(AAXS)以及各種設備(包括 [維德文](https://www.widevine.com) 在Chrome和Android上， [公平遊戲](https://developer.apple.com/streaming/fps/) 在薩法里和iOS [播放就緒](https://www.microsoft.com/playready/) 在Edge和XboxOne上。 請咨詢Adobe代表，瞭解這些平台上當前有哪些DRM方案以及將來發佈的預定日期。

TVSDK支援由使用這些協定的任何許可證伺服器頒發的DRM許可證。 除了支援多個DRM解決方案外，Adobe還提供 *由ExpressPlay提供支援的黃金時段DRM雲* ExpressPlay為每個解決方案運行許可證伺服器的解決方案。 這可以簡化DRM許可證頒發需要的設定和維護。

要使用 *由ExpressPlay提供支援的黃金時段DRM雲* 要在TVSDK應用中實現DRM需求，必須首先獲取 [ExpressPlay.com](https://www.expressplay.com) 帳戶。 ExpressPlay為幾種不同的DRM保護方案提供許可功能，還提供包裝和密鑰管理等其他服務。

您的Adobe代表將首先設定您的ExpressPlay帳戶。 然後，您可以配置帳戶並獲取 *客戶身份驗證器* 用於向ExpressPlay伺服器發出許可證令牌請求。
