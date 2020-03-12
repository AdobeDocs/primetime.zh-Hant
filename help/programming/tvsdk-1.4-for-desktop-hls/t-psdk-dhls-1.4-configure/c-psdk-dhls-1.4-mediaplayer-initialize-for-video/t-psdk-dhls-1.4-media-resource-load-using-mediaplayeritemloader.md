---
description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
seo-description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
seo-title: 使用MediaPlayerItemLoader載入媒體資源
title: 使用MediaPlayerItemLoader載入媒體資源
uuid: a7ec8f58-7357-4757-a402-e879dd6caec8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用MediaPlayerItemLoader載入媒體資源{#load-a-media-resource-using-mediaplayeritemloader}

解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。

通過類 `MediaPlayerItemLoader` 別，您可以交換對應的媒體資源，而不將視圖附加到 `MediaPlayerItem``MediaPlayer` 實例，這會導致視頻解碼硬體資源的分配。 獲取實例的過 `MediaPlayerItem` 程是非同步的。

1. 為這些事件實施事件偵聽 `MediaPlayerItemLoader` 器：

   * `MediaPlayerItemLoaderEvent.ERROR` 事件

      TVSDK會使用此項來通知您的應用程式發生錯誤。 TVSDK提供包含診斷資訊的錯誤屬性。

1. 將此實例註冊到 `MediaPlayerItemLoader`。
1. 呼 `DefaultMediaPlayerItemLoader.load`叫，傳遞物件的例 `MediaResource` 項。

   物件的URL `MediaResource` 必須指向您要取得資訊的串流。 例如：

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

