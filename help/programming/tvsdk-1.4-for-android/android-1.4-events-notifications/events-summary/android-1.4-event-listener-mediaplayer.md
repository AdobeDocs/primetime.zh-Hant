---
description: TVSDK響應於廣告相關操作（例如當廣告開始播放時）來調度廣告回放事件。
title: 廣告播放事件
exl-id: f35e3c6f-1d58-4498-9e3b-cbd53e573ef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 廣告播放事件{#ad-playback-events}

TVSDK響應於廣告相關操作（例如當廣告開始播放時）來調度廣告回放事件。

要獲得有關所有廣告播放相關事件的通知，請註冊 `MediaPlayer.AdPlaybackEventListener` 包括以下回調。

>[!TIP]
>
>當廣告插入媒體或從媒體中刪除時，TVSDK將調度播放事件 [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated())。

| 事件 | 意義 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 廣告的斷續已經完全播放了。 |
| onAdBreakSkpited | 播放期間跳過了廣告中斷。 |
| [在AdBreakStart上](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 廣告斷開。 |
| [在AdClick上](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak、Ad ad、AdClick adClick) | 用戶已按一下該廣告。 向應用程式提供有關用戶按一下的廣告的資訊，以響應應用程式調用 `notifyClick` 的 `MediaPlayerView`。 |
| [在AdComplete上](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak、Ad ad) | 一個廣告已經播放完。 |
| [AdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) （AdBreak adBreak、Ad ad、int百分比） | 廣告播放已進行。 在廣告播放時多次發送。 |
| [在AdStart上](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak、Ad ad) | 廣告已經開始。 |
