---
description: MediaPlayerItem.timedMetadata屬性允許您訪問從播放清單/清單標籤或從媒體流中的ID3標籤建立的所有TimedMetadata對象。 MediaPlayerItem.hasTimedMetadata屬性指示當前媒體中是否存在訂閱的自定義標籤。
title: 清單標籤的通知
exl-id: 1a91fa47-edd5-4496-9755-17c906a3cf54
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性允許您訪問從播放清單/清單標籤或從媒體流中的ID3標籤建立的所有TimedMetadata對象。 MediaPlayerItem.hasTimedMetadata屬性指示當前媒體中是否存在訂閱的自定義標籤。

您可以通過偵聽以下事件來監視定時元資料，這些事件會通知您的應用程式相關活動：

* `MediaPlayerItemEvent.ITEM_CREATED`:初始清單 `TimedMetadata` 對象在 `MediaPlayerItem` 的子菜單。 發生此情況時，此事件會通知您的應用程式。

* `MediaPlayerItemEvent.ITEM_UPDATED`:對於清單/播放清單定期刷新的即時/線性流，更新的播放清單/清單中可能會出現附加的自定義標籤，因此可能會將附加的TimedMetadata對象添加到 `MediaPlayerItem.timedMetadata` 屬性。 發生此情況時，此事件會通知您的應用程式。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次新 `TimedMetadata` 建立對象，此事件由 `MediaPlayer`。 未為 `TimedMetadata` 在初始化階段建立的對象。
