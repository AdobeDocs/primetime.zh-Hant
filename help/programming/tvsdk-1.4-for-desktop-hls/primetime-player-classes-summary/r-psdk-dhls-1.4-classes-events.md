---
description: 這些類別說明TVSDK為回應各種活動而將事件派單至您的媒體播放器。
seo-description: 這些類別說明TVSDK為回應各種活動而將事件派單至您的媒體播放器。
seo-title: 事件類別
title: 事件類別
uuid: 5e63d43c-6112-4958-b8cd-ccf123affd08
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# 事件類{#events-classes}

這些類別說明TVSDK為回應各種活動而將事件派單至您的媒體播放器。

套件：[com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 名稱 | 意義 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 類別。 廣告插播開始或完成。 |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 類別。 使用者按一下廣告。 |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 類別。 玩家播放廣告。 |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 類別。 播放器啟動或停止緩衝。 |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | 類別。 播放器會顯示自訂廣告載入狀態，並可忽略有錯誤或載入時間過長的廣告。 |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 類別。 新的DRM元資料與當前項相關聯。 |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 類別。 目前播放的媒體串流有下載資訊。 |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 類別。 已建立媒體播放器項目。 |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 類別。 載入操作已完成。 由`MediaPlayerItemLoader`派送以通知其客戶。 |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 類別。 媒體播放器狀態已變更。 |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 類別。 已點按`MediaPlayerView`。 |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 類別。 媒體播放器的播放速率會變更。 |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 類別。 由於網路或機器狀況，媒體播放器的自適應位速率切換算法已切換到另一個配置檔案。 |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 類別。 玩家開始搜尋，或搜尋作業完成。 |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 類別。 視訊大小可供使用。 |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 類別。 媒體播放器的狀態已變更。 |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 類別。 機會檢測器處理定時元資料。 |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 類別。 媒體播放器時間軸已變更。 |