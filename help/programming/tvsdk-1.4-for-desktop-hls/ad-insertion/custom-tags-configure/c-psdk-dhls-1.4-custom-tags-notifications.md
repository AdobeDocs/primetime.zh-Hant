---
description: MediaPlayerItem.timedMetadata屬性可讓您存取從播放清單/資訊清單標籤或媒體串流中的ID3標籤建立的所有TimedMetadata物件。 MediaPlayerItem.hasTimedMetadata屬性指出目前媒體中是否有訂閱的自訂標籤。
title: 資訊清單標籤的通知
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 資訊清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性可讓您存取從播放清單/資訊清單標籤或媒體串流中的ID3標籤建立的所有TimedMetadata物件。 MediaPlayerItem.hasTimedMetadata屬性指出目前媒體中是否有訂閱的自訂標籤。

您可以監聽下列事件來監視定時中繼資料，這些事件會通知您的應用程式相關活動：

* `MediaPlayerItemEvent.ITEM_CREATED`：初始清單 `TimedMetadata` 物件可在 `MediaPlayerItem` 「 」已建立。 此事件會在發生時通知您的應用程式。

* `MediaPlayerItemEvent.ITEM_UPDATED`：針對資訊清單/播放清單定期重新整理的即時/線性資料流，更新的播放清單/資訊清單中可能會顯示其他自訂標籤，因此其他TimedMetadata物件可能會新增至 `MediaPlayerItem.timedMetadata` 屬性。 此事件會在發生時通知您的應用程式。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`：每當新的 `TimedMetadata` 物件建立後，此事件會由 `MediaPlayer`. 此事件不會分派給 `TimedMetadata` 在初始化階段建立的物件。
