---
description: TVSDK會根據廣告相關作業（例如廣告開始播放時）來調度廣告播放事件。
title: 廣告播放事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# 廣告播放事件{#ad-playback-events}

TVSDK會根據廣告相關作業（例如廣告開始播放時）來調度廣告播放事件。

要獲得有關所有廣告播放相關事件的通知，請向`MediaPlayer`對象註冊以下事件的監聽器。

>[!TIP]
>
>當廣告插入媒體或從媒體移除時，TVSDK會調度播放事件TimelineEvent。[時間軸_已更新](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED)。

| 事件 | 意義 |
|---|---|
| AdBreakPlaybackEvent。[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 廣告插播已完全播放。 |
| AdBreakPlaybackEvent。[AD_BREAK_BRIKPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 在播放期間會略過廣告插播。 |
| AdBreakPlaybackEvent。[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 廣告插播已開始。 |
| AdClickEvent。[廣告_點按](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 使用者已點按廣告。 針對您的應用程式在`MediaPlayerView`上呼叫`notifyClick`，提供使用者所點按廣告的相關資訊給您的應用程式。 |
| AdPlaybackEvent。[廣告完成(_COMPLETED)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 廣告已完全播放。 |
| AdPlaybackEvent。[廣告進度](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 廣告播放已進行。 在廣告播放時多次傳送。 |
| AdPlaybackEvent。[廣告_搜尋](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 跨廣告界限或廣告內發生搜尋。 |
| AdPlaybackEvent。[AD _STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 廣告已開始。 |