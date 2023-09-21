---
description: TVSDK會傳送廣告播放事件來回應廣告相關的操作，例如當廣告開始播放時。
title: 廣告播放事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 廣告播放事件 {#ad-playback-events}

TVSDK會傳送廣告播放事件來回應廣告相關的操作，例如當廣告開始播放時。

若要收到有關所有廣告播放相關事件的通知，請使用 `MediaPlayer` 物件。

>[!TIP]
>
>當廣告插入媒體或從媒體中移除時，TVSDK會傳送播放事件TimelineEvent。[時間軸已更新](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| 事件 | 含義 |
|---|---|
| AdBreakPlaybackEvent。[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 廣告插播已完全播放。 |
| AdBreakPlaybackEvent。[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 錄放期間已略過廣告插播。 |
| AdBreakPlaybackEvent。[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 廣告插播已開始。 |
| AdClickEvent。[廣告點按(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 使用者已按一下廣告。 將使用者點按之廣告的相關資訊提供給您的應用程式，以回應您的應用程式呼叫 `notifyClick` 於 `MediaPlayerView`. |
| AdPlaybackEvent。[廣告已完成(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 廣告已完全播放。 |
| AdPlaybackEvent。[廣告進度(_P)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 廣告播放已進行中。 在廣告播放時傳送多次。 |
| AdPlaybackEvent。[AD SEEK(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 搜尋已發生於廣告邊界或廣告內。 |
| AdPlaybackEvent。[廣告已開始(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 廣告已開始。 |
