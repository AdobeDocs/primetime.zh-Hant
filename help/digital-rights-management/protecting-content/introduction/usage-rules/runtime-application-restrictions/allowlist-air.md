---
title: 允許播放受保護內容的Primetime DRM應用程式清單
description: 允許播放受保護內容的Primetime DRM應用程式清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 允許播放受保護內容{#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}的Primetime DRM應用程式的清單

允許清單會指定允許播放內容的AIR、iOS和Android應用程式。 它也會指定AIR和iOS應用程式ID、最低版本、最高版本和發佈者ID。

範例使用案例：使用此規則可限制特定應用程式的播放，或控制可存取內容的應用程式版本。

>[!NOTE]
>
>如果您使用AdobeFlash Builder來建立受保護的應用程式，您必須確定您未在除錯模式中部署應用程式。 當您在除錯模式中部署應用程式時，Flash Builder會附加`.debug`至AIR應用程式ID，如此會造成Primetime DRM中的允許清單功能意外運作。
