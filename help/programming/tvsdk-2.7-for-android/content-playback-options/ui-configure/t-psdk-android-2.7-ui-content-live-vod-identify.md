---
description: 您可能需要知道媒體內容是即時或隨選視訊(VOD)。
seo-description: 您可能需要知道媒體內容是即時或隨選視訊(VOD)。
seo-title: 識別內容是即時或VOD
title: 識別內容是即時或VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 識別內容是即時或VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時或隨選視訊(VOD)。

1. 請確定播放器至少處於`PREPARED`狀態。
1. 判斷`MediaPlayerItem`內容是即時(`true`)還是VOD(`false`)。

   ```java
   boolean isLive();
   ```
