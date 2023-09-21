---
title: 允許播放受保護內容的Primetime DRM應用程式清單
description: 允許播放受保護內容的Primetime DRM應用程式清單
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 允許播放受保護內容的Primetime DRM應用程式清單 {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

允許清單會指定允許播放內容的AIR、iOS和Android應用程式。 也會指定AIR和iOS應用程式ID、最低版本、最高版本和發佈者ID。

使用案例範例：使用此規則將播放限制在特定應用程式，或控制可存取內容的應用程式版本。

>[!NOTE]
>
>如果您使用AdobeFlash Builder來建置受保護的應用程式，您必須確定不要在偵錯模式中部署應用程式。 當您在偵錯模式下部署應用程式時，Flash Builder會附加 `.debug` AIR應用程式ID，而這會導致Primetime DRM中的允許清單功能出現意外行為。
