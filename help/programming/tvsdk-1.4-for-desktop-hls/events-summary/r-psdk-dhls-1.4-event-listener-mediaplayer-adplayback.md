---
description: TVSDK響應於廣告相關操作（例如當廣告開始播放時）來調度廣告回放事件。
title: 廣告播放事件
exl-id: 61e7c9ec-20ed-4221-8ae7-b5d43adb4ce4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 廣告播放事件 {#ad-playback-events}

TVSDK響應於廣告相關操作（例如當廣告開始播放時）來調度廣告回放事件。

要獲得有關所有廣告播放相關事件的通知，請向 `MediaPlayer` 對象。

>[!TIP]
>
>當廣告插入媒體或從媒體中刪除時，TVSDK將調度播放事件TimelineEvent。[時間軸_已更新](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED)。

| 事件 | 意義 |
|---|---|
| AdBreakPlaybackEvent。[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 廣告的斷續已經完全播放了。 |
| AdBreakPlaybackEvent。[跳過AD_BREAK_SKPITED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 播放期間跳過了廣告中斷。 |
| AdBreakPlaybackEvent。[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 廣告斷開。 |
| AdClickEvent。[廣告按一下(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 用戶已按一下該廣告。 向應用程式提供有關用戶按一下的廣告的資訊，以響應應用程式調用 `notifyClick` 的 `MediaPlayerView`。 |
| AdPlaybackEvent。[已完成廣告(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 一個廣告已經播放完。 |
| AdPlaybackEvent。[廣告進度(_P)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 廣告播放已進行。 在廣告播放時多次發送。 |
| AdPlaybackEvent。[尋道(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 在廣告邊界或廣告內發生搜索。 |
| AdPlaybackEvent。[已啟動廣告(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 廣告已經開始。 |
