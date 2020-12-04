---
description: 在某些情況下，您需要知道媒體內容是即時或VOD。
seo-description: 在某些情況下，您需要知道媒體內容是即時或VOD。
seo-title: 識別內容是即時或VOD
title: 識別內容是即時或VOD
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 識別內容是即時或VOD{#identify-whether-the-content-is-live-or-vod}

在某些情況下，您需要知道媒體內容是即時或VOD。

1. 請確定播放器至少處於「已初始化」狀態。
1. 判斷`MediaPlayerItem`內容是即時(true)還是VOD(false)。

   ```
   function get isLive():Boolean;
   ```

