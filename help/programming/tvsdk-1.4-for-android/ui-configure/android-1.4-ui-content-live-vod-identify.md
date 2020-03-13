---
description: 在某些情況下，您需要知道媒體內容是即時或VOD。
seo-description: 在某些情況下，您需要知道媒體內容是即時或VOD。
seo-title: 識別內容是即時或VOD
title: 識別內容是即時或VOD
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 識別內容是即時或VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是即時或VOD。

1. 確保玩家至少處於PREPARED狀態。
1. 判斷內容 `MediaPlayerItem` 是即時(true)還是VOD(false)。

   ```java
   boolean isLive();
   ```

