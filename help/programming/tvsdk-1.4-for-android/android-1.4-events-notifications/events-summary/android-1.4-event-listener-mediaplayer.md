---
description: TVSDK會根據廣告相關作業（例如廣告開始播放時）來調度廣告播放事件。
title: 廣告播放事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 廣告播放事件{#ad-playback-events}

TVSDK會根據廣告相關作業（例如廣告開始播放時）來調度廣告播放事件。

若要獲得所有廣告播放相關事件的通知，請註冊`MediaPlayer.AdPlaybackEventListener`的實作，包括下列回呼。

>[!TIP]
>
>當廣告插入媒體或從媒體移除時，TVSDK會調度播放事件[ onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated())。

| 事件 | 意義 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 廣告插播已完全播放。 |
| onAdBreakKlipted | 在播放期間會略過廣告插播。 |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 廣告插播已開始。 |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) （AdBreak adBreak、廣告、AdClick adClick） | 使用者已點按廣告。 針對您的應用程式在`MediaPlayerView`上呼叫`notifyClick`，提供使用者所點按廣告的相關資訊給您的應用程式。 |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) （AdBreak adBreak、廣告） | 廣告已完全播放。 |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) （AdBreak adBreak、廣告、int百分比） | 廣告播放已進行。 在廣告播放時多次傳送。 |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) （AdBreak adBreak、廣告） | 廣告已開始。 |