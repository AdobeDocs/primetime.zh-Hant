---
description: 解析媒體資源的另一種方法是使用MediaPlayerItemLoader。 當您希望獲取有關特定媒體流的資訊而不實例化MediaPlayer實例時，此功能非常有用。
title: 使用MediaPlayerItemLoader載入媒體資源
exl-id: 08379bd8-1602-4013-a6fb-b1aa6ba539aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader載入媒體資源{#load-a-media-resource-using-mediaplayeritemloader}

解析媒體資源的另一種方法是使用MediaPlayerItemLoader。 當您希望獲取有關特定媒體流的資訊而不實例化MediaPlayer實例時，此功能非常有用。

通過 `MediaPlayerItemLoader` 類，可以為相應的 `MediaPlayerItem` 不將視圖附加到 `MediaPlayer` 實例，這將導致視頻解碼硬體資源的分配。 獲取 `MediaPlayerItem` 實例是非同步的。

1. 實現這些事件偵聽器 `MediaPlayerItemLoader` 事件：

   * `MediaPlayerItemLoaderEvent.ERROR` 事件

      TVSDK使用此功能通知您的應用程式發生錯誤。 TVSDK提供包含診斷資訊的錯誤屬性。

1. 將此實例註冊到 `MediaPlayerItemLoader`。
1. 呼叫 `DefaultMediaPlayerItemLoader.load`，傳遞 `MediaResource` 的雙曲餘切值。

   的URL `MediaResource` 對象必須指向要獲取資訊的流。 例如：

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```
