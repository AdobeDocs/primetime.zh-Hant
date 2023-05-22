---
title: 允許允許Mighine DRM應用程式播放受保護內容的清單
description: 允許允許Mighine DRM應用程式播放受保護內容的清單
copied-description: true
exl-id: c5aced0f-2c38-4ae7-9a33-44877e57a993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 允許允許Mighine DRM應用程式播放受保護內容的清單 {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

允許清單指定允許播放內容的AIR、iOS和Android應用程式。 它還指定AIR和iOS應用程式ID、最低版本、最高版本和發佈者ID。

示例用例：使用此規則可限制特定應用程式的回放，或控制可以訪問內容的應用程式的版本。

>[!NOTE]
>
>如果使用AdobeFlash Builder構建受保護的應用程式，則必須確保未在調試模式下部署應用程式。 在調試模式下部署應用程式時，Flash Builder會附加 `.debug` 到AIR應用程式ID，這會導致黃金時段DRM中的允許清單功能出現意外行為。
