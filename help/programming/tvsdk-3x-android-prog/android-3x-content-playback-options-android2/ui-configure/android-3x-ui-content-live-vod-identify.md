---
description: 您可能需要知道媒體內容為即時或視訊點播(VOD)。
title: 識別內容為即時或VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# 識別內容為即時或VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容為即時或視訊點播(VOD)。

1. 確保播放器至少在 `PREPARED` 州別。
1. 確定 `MediaPlayerItem` 內容已上線( `true`)或VOD ( `false`)。

   ```java
   boolean isLive();
   ```
