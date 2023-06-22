---
description: 解析媒體資源的另一種方式是使用MediaPlayerItemLoader。 如果您想要取得特定媒體資料流的相關資訊，但不具現化MediaPlayer執行個體，這個功能會很有用。
title: 使用MediaPlayerItemLoader載入媒體資源
exl-id: 08379bd8-1602-4013-a6fb-b1aa6ba539aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader載入媒體資源{#load-a-media-resource-using-mediaplayeritemloader}

解析媒體資源的另一種方式是使用MediaPlayerItemLoader。 如果您想要取得特定媒體資料流的相關資訊，但不具現化MediaPlayer執行個體，這個功能會很有用。

透過 `MediaPlayerItemLoader` 類別時，您可以交換媒體資源以取得對應的 `MediaPlayerItem` 而不將檢視附加至 `MediaPlayer` 執行個體，這會配置視訊解碼硬體資源。 取得「 」的程式 `MediaPlayerItem` 執行個體為非同步。

1. 實作這些專案的事件接聽程式 `MediaPlayerItemLoader` 事件：

   * `MediaPlayerItemLoaderEvent.ERROR` 事件

      TVSDK會使用此功能，通知您的應用程式已發生錯誤。 TVSDK提供的錯誤屬性包含診斷資訊。

1. 將此執行個體註冊至 `MediaPlayerItemLoader`.
1. 呼叫 `DefaultMediaPlayerItemLoader.load`，傳遞例項 `MediaResource` 物件。

   的URL `MediaResource` 物件必須指向您要取得資訊的資料流。 例如：

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
