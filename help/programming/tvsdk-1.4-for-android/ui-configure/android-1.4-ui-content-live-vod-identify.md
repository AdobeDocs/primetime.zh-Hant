---
description: 在某些情況下，您需要知道媒體內容是即時還是VOD。
title: 識別內容為即時或VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 識別內容為即時或VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是即時還是VOD。

1. 請確定播放器至少處於「已準備」狀態。
1. 確定 `MediaPlayerItem` 內容為即時(true)或VOD (false)。

   ```java
   boolean isLive();
   ```
