---
description: 您可能需要知道媒體內容是即時或隨選視訊(VOD)。
title: 識別內容是即時或VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# 識別內容是即時或VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時或隨選視訊(VOD)。

1. 請確定播放器至少處於`PREPARED`狀態。
1. 判斷`MediaPlayerItem`內容是即時(`true`)還是VOD(`false`)。

   ```java
   boolean isLive();
   ```
