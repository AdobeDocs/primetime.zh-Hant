---
description: 這些類別會說明TVSDK為回應各種活動而排程至您的媒體播放器的事件。
title: 事件類別
exl-id: a349984a-5e47-4895-a56f-ef25eb372c79
source-git-commit: 776d3d1668f063f1595bd3ecb53603171905014a
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 事件類別 {#events-classes}

這些類別會說明TVSDK為回應各種活動而排程至您的媒體播放器的事件。

封裝： [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 名稱 | 含義 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 類別。 廣告插播開始或完成。 |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 類別。 使用者已點選廣告。 |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 類別。 播放器已播放廣告。 |
| [緩衝事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 類別。 播放器已啟動或停止緩衝。 |
| [CustomAdevent](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-1-4-for-desktop-hls/advertising/custom-ads/r-psdk-dhls-1.4-custom-ad-events.html?lang=en) | 類別。 播放器會顯示自訂廣告載入狀態，並且可以忽略有錯誤或載入時間過長的廣告。 |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 類別。 新的DRM中繼資料與目前專案相關聯。 |
| [loadinformevent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 類別。 目前播放的媒體資料流有下載資訊可用。 |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 類別。 已建立媒體播放器專案。 |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 類別。 載入作業已完成。 傳送者 `MediaPlayerItemLoader` 以通知其使用者端。 |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 類別。 媒體播放器狀態已變更。 |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 類別。 此 `MediaPlayerView` 已按一下。 |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 類別。 媒體播放器的播放速率會變更。 |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 類別。 由於網路或電腦狀況，媒體播放器的最適化位元速率切換演演算法已切換至另一個設定檔。 |
| [搜尋事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 類別。 播放器已開始搜尋或搜尋作業已完成。 |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 類別。 視訊大小可供使用。 |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 類別。 媒體播放器的狀態已變更。 |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 類別。 機會偵測器會處理定時中繼資料。 |
| [時間軸事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 類別。 媒體播放器時間軸已變更。 |
