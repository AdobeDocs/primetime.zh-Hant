---
description: 您可能需要知道媒體內容是即時或隨選視訊(VOD)。
seo-description: 您可能需要知道媒體內容是即時或隨選視訊(VOD)。
seo-title: 識別內容是即時或VOD
title: 識別內容是即時或VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 識別內容是即時或VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時或隨選視訊(VOD)。

1. 請確定玩家至少處於狀 `PREPARED` 態。
1. 判斷內 `MediaPlayerItem` 容是即時( `true`)還是VOD( `false`)。

   ```java
   boolean isLive();
   ```
