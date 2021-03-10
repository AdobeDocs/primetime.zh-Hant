---
description: 在某些情況下，您需要知道媒體內容是即時或VOD。
title: 識別內容是即時或VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# 識別內容是即時或VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是即時或VOD。

1. 請確定播放器至少處於「已初始化」狀態。
1. 判斷`MediaPlayerItem`內容是即時(true)還是VOD(false)。

   ```
   function get isLive():Boolean;
   ```

