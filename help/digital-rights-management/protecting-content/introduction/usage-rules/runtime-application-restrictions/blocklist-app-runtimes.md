---
description: 'null'
seo-description: 'null'
seo-title: 應用程式執行時期的區塊清單
title: 應用程式執行時期的區塊清單
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 應用程式執行時期的區塊清單 {#blocklist-of-application-runtimes}

應用程式執行階段的區塊清單會指定無法存取內容的Primetime用戶端或Flash執行階段版本。 指定受限制的執行時期（Flash Player、AIR或iOS）、平台和版本。

範例使用案例： 與Primetime DRM用戶端區塊清單類似，最新版本的Flash Player、AIR或iOS執行時期可指定為取得授權和內容播放所需的最低版本。

除了下列屬性外，您還可以依據Primetime DRM用戶端版本支援的任何屬性來識別應用程式執行時期：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 應用程式 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 完全符合 | 識別應用程式執行時期的名稱。 |

