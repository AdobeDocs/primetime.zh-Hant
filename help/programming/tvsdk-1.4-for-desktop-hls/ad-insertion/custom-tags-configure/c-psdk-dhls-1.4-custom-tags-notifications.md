---
description: MediaPlayerItem.timedMetadata屬性可讓您存取從播放清單／資訊清單標籤或從媒體串流內的ID3標籤建立的所有TimedMetadata物件。 MediaPlayerItem.hasTimedMetadata屬性可指出目前媒體中是否有已訂閱的自訂標籤。
seo-description: MediaPlayerItem.timedMetadata屬性可讓您存取從播放清單／資訊清單標籤或從媒體串流內的ID3標籤建立的所有TimedMetadata物件。 MediaPlayerItem.hasTimedMetadata屬性可指出目前媒體中是否有已訂閱的自訂標籤。
seo-title: 資訊清單標籤的通知
title: 資訊清單標籤的通知
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 資訊清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性可讓您存取從播放清單／資訊清單標籤或從媒體串流內的ID3標籤建立的所有TimedMetadata物件。 MediaPlayerItem.hasTimedMetadata屬性可指出目前媒體中是否有已訂閱的自訂標籤。

您可以監聽下列事件來監控計時中繼資料，這些事件會通知您的應用程式相關活動：

* `MediaPlayerItemEvent.ITEM_CREATED`:在建立對象 `TimedMetadata` 後，可以使用對象的 `MediaPlayerItem` 初始清單。 發生此情況時，此事件會通知您的應用程式。

* `MediaPlayerItemEvent.ITEM_UPDATED`:對於資訊清單／播放清單定期重新整理的即時／線性串流，更新的播放清單／資訊清單中可能會顯示其他自訂標籤，因此可能會將其他TimedMetadata物件新增至屬 `MediaPlayerItem.timedMetadata` 性。 發生此情況時，此事件會通知您的應用程式。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次建立新對 `TimedMetadata` 像時，都會由調度此事件 `MediaPlayer`。 在初始化階段中建立的對 `TimedMetadata` 像不會調度此事件。

