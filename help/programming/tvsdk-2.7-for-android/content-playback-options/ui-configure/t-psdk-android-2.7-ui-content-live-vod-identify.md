---
description: 您可能需要知道媒體內容是即時的還是視頻點播(VOD)。
title: 確定內容是即時還是VOD
exl-id: 756d4f04-d354-4194-80c9-c2ea6198a566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# 確定內容是即時還是VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時的還是視頻點播(VOD)。

1. 確保玩家至少位於 `PREPARED` 狀態。
1. 確定 `MediaPlayerItem` 內容為活動( `true`)或VOD( `false`)。

   ```java
   boolean isLive();
   ```
