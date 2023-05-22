---
description: 在某些情況下，您需要知道媒體內容是實況還是視頻點播。
title: 確定內容是即時還是VOD
exl-id: 180eb515-5bc1-4b32-babf-bcc640ebfa72
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 確定內容是即時還是VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是實況還是視頻點播。

1. 確保播放器至少處於「已初始化」狀態。
1. 確定 `MediaPlayerItem` 內容為即時(true)或VOD(false)。

   ```
   function get isLive():Boolean;
   ```
