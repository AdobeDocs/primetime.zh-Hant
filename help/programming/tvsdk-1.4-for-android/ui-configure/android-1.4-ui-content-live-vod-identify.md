---
description: 在某些情況下，您需要知道媒體內容是實況還是視頻點播。
title: 確定內容是即時還是VOD
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 確定內容是即時還是VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是實況還是視頻點播。

1. 確保玩家至少處於PREPARED狀態。
1. 確定 `MediaPlayerItem` 內容為即時(true)或VOD(false)。

   ```java
   boolean isLive();
   ```
