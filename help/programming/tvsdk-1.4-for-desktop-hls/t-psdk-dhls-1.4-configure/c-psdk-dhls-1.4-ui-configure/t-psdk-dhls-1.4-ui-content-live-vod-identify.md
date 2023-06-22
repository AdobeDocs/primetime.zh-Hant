---
description: 在某些情況下，您需要知道媒體內容是即時還是VOD。
title: 識別內容為即時或VOD
exl-id: 180eb515-5bc1-4b32-babf-bcc640ebfa72
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 識別內容為即時或VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是即時還是VOD。

1. 請確定播放器至少處於INITIALIZED狀態。
1. 決定 `MediaPlayerItem` 內容為即時(true)或VOD (false)。

   ```
   function get isLive():Boolean;
   ```
