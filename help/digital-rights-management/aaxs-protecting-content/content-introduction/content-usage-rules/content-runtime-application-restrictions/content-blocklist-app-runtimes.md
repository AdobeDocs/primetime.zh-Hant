---
title: 限制存取受保護內容之應用程式執行時期的區塊清單
description: 限制存取受保護內容之應用程式執行時期的區塊清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 限制存取受保護內容的應用程式執行時期區塊清單{#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定無法存取內容的Primetime或Flash執行階段版本。 指定受限制的執行時期(Flash Player、AIR或iOS)、平台和版本。

範例使用案例：與DRM用戶端區塊清單類似，Flash Player、AIR或iOS執行時期的最新版本可指定為取得授權和內容播放所需的最低版本。

除了下列屬性外，應用運行時還可由DRM客戶端版本支援的任何屬性來標識：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 應用程式 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 完全符合 | 識別應用程式執行時期的名稱。 |
