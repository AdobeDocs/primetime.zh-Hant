---
description: 您可能需要知道媒體內容為即時或隨選影片(VOD)。
title: 識別內容為即時或VOD
exl-id: a75332d9-a23a-423c-8d1f-81b40ca73b21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# 識別內容為即時或VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容為即時或隨選影片(VOD)。

1. 確保播放器至少在 `PREPARED` 州別。
1. 決定 `MediaPlayerItem` 內容已上線( `true`)或VOD ( `false`)。

   ```java
   boolean isLive();
   ```
