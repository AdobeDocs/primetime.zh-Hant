---
description: 若要接收資訊清單中標籤的相關通知，請註冊適當的事件監聽器。
title: 為定時中繼資料通知新增接聽程式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 為定時中繼資料通知新增接聽程式{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的相關通知，請註冊適當的事件監聽器。

您可以監聽下列事件來監視定時中繼資料，這些事件會通知您的應用程式相關活動：

* `MediaPlayerItemEvent.ITEM_CREATED`：初始清單 `TimedMetadata` 物件可在 `MediaPlayerItem` 「 」已建立。

  此事件會在發生時通知您的應用程式。

* `MediaPlayerItemEvent.ITEM_UPDATED`：針對資訊清單/播放清單定期重新整理的即時/線性資料流，更新的播放清單/資訊清單中可能會顯示其他自訂標籤，因此也會顯示其他自訂標籤 `TimedMetadata` 物件可新增至 `MediaPlayerItem.timedMetadata` 屬性。

  此事件會在發生時通知您的應用程式。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`：每次使用 `TimedMetadata` 物件建立後，此事件會由MediaPlayer傳送。

  此事件不會分派給 `TimedMetadata` 在初始化階段建立的物件。

1. 實作適當的接聽程式。

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. 註冊事件接聽程式。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

ID3中繼資料會透過相同的傳送 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. 不過，這應該不會造成任何混淆，因為您可以使用TimedMetadata物件的 `type` 屬性以區分TAG和ID3。 如需ID3標籤的詳細資訊，請參閱 [ID3標籤](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
