---
description: 解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。
title: 使用MediaPlayerItemLoader載入媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# 使用MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}載入媒體資源

解決媒體資源的另一種方式是使用MediaPlayerItemLoader。 當您想要取得特定媒體串流的相關資訊而不執行個體化MediaPlayer例項時，這個功能會很有用。

通過`MediaPlayerItemLoader`類，您可以為相應的`MediaPlayerItem`交換媒體資源，而不將視圖附加到`MediaPlayer`實例，這將導致視頻解碼硬體資源的分配。 獲取`MediaPlayerItem`實例的過程是非同步的。

1. 為以下`MediaPlayerItemLoader`事件實施事件偵聽器：

   * `MediaPlayerItemLoaderEvent.ERROR` 事件

      TVSDK會使用此項來通知您的應用程式發生錯誤。 TVSDK提供包含診斷資訊的錯誤屬性。

1. 將此實例註冊到`MediaPlayerItemLoader`。
1. 呼叫`DefaultMediaPlayerItemLoader.load`，傳遞`MediaResource`物件的例項。

   `MediaResource`物件的URL必須指向您要取得資訊的串流。 例如：

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

