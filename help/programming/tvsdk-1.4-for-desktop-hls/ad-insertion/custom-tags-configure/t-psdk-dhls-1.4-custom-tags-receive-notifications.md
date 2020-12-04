---
description: 若要接收資訊清單中標籤的通知，請註冊適當的事件接聽程式。
seo-description: 若要接收資訊清單中標籤的通知，請註冊適當的事件接聽程式。
seo-title: 新增計時中繼資料通知的監聽器
title: 新增計時中繼資料通知的監聽器
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 為計時中繼資料通知新增監聽器{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的通知，請註冊適當的事件接聽程式。

您可以監聽下列事件來監控計時中繼資料，這些事件會通知您的應用程式相關活動：

* `MediaPlayerItemEvent.ITEM_CREATED`:在建立對象 `TimedMetadata` 後，可以使用對象 `MediaPlayerItem` 的初始清單。

   發生此情況時，此事件會通知您的應用程式。

* `MediaPlayerItemEvent.ITEM_UPDATED`:對於資訊清單／播放清單定期重新整理的即時／線性串流，更新的播放清單／資訊清單中可能會顯示其他自訂標籤， `TimedMetadata` 因此可能會將其他物件新增至 `MediaPlayerItem.timedMetadata` 屬性。

   發生此情況時，此事件會通知您的應用程式。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次建立新 `TimedMetadata` 物件時，MediaPlayer就會傳送此事件。

   對於在初始化階段建立的`TimedMetadata`對象，不會調度此事件。

1. 實作適當的監聽器。

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

1. 註冊事件偵聽器。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

ID3中繼資料會透過相同的`TimedMetadataEvent.TIMED_METADATA_AVAILABLE`傳送。 但是，這不會造成任何混淆，因為您可以使用TimedMetadata物件的`type`屬性來區分TAG和ID3。 如需ID3標籤的詳細資訊，請參閱[ID3標籤](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md)。