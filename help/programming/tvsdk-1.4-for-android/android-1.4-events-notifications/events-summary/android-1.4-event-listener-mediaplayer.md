---
description: TVSDK會傳送廣告播放事件以回應與廣告相關的操作，例如當廣告開始播放時。
title: 廣告播放事件
exl-id: f35e3c6f-1d58-4498-9e3b-cbd53e573ef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 廣告播放事件{#ad-playback-events}

TVSDK會傳送廣告播放事件以回應與廣告相關的操作，例如當廣告開始播放時。

若要收到所有廣告播放相關事件的通知，請註冊實作 `MediaPlayer.AdPlaybackEventListener` 包含下列回呼。

>[!TIP]
>
>當廣告插入媒體或從中移除時，TVSDK會傳送播放事件 [時間軸上已更新](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| 事件 | 含義 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 廣告插播已完全播放。 |
| onAdBreakSkip | 播放期間已略過廣告插播。 |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 廣告插播已開始。 |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) （AdBreak adBreak、廣告、AdClick adClick） | 使用者已按一下廣告。 將使用者點按的廣告相關資訊提供給您的應用程式，以回應您的應用程式呼叫 `notifyClick` 於 `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) （AdBreak adBreak、廣告） | 廣告已完全播放。 |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) （AdBreak adBreak、廣告廣告、整數百分比） | 廣告播放已取得進展。 在廣告播放時傳送多次。 |
| [onAdSt](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) （AdBreak adBreak、廣告） | 廣告已開始。 |
