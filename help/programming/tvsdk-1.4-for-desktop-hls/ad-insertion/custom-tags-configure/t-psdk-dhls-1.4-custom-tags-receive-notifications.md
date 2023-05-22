---
description: 要接收有關清單中標籤的通知，請註冊相應的事件偵聽器。
title: 為定時元資料通知添加偵聽器
exl-id: 1df8a4fc-8368-4a80-8f8b-00c1207e6602
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 為定時元資料通知添加偵聽器{#add-listeners-for-timed-metadata-notifications}

要接收有關清單中標籤的通知，請註冊相應的事件偵聽器。

您可以通過偵聽以下事件來監視定時元資料，這些事件會通知您的應用程式相關活動：

* `MediaPlayerItemEvent.ITEM_CREATED`:初始清單 `TimedMetadata` 對象在 `MediaPlayerItem` 的子菜單。

   發生此情況時，此事件會通知您的應用程式。

* `MediaPlayerItemEvent.ITEM_UPDATED`:對於清單/播放清單定期刷新的即時/線性流，更新的播放清單/清單中可能會出現附加的自定義標籤，因此附加的 `TimedMetadata` 對象可能已添加到 `MediaPlayerItem.timedMetadata` 屬性。

   發生此情況時，此事件會通知您的應用程式。

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:每次新 `TimedMetadata` 對象已建立，此事件由MediaPlayer調度。

   未為 `TimedMetadata` 在初始化階段建立的對象。

1. 實施適當的偵聽器。

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

ID3元資料通過同一 `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`。 但是，這不應引起任何混淆，因為您可以使用TimedMetadata對象 `type` 用於區分TAG和ID3的屬性。 有關ID3標籤的詳細資訊，請參見 [ID3標籤](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md)。
