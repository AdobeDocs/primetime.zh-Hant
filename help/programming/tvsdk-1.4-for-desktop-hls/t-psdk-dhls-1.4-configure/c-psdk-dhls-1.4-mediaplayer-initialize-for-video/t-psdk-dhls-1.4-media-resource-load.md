---
description: 直接將MediaResource實體化並載入要播放的視訊內容，以載入資源。 這是載入媒體資源的其中一種方式。
title: 在MediaPlayer中載入媒體資源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源{#load-a-media-resource-in-the-mediaplayer}

直接將MediaResource實體化並載入要播放的視訊內容，以載入資源。 這是載入媒體資源的其中一種方式。

1. 設定您的 `MediaPlayer` 物件的可播放專案，以及要播放的新資源。

   呼叫，取代您現有的MediaPlayer目前可播放的專案 `MediaPlayer.replaceCurrentResource` 並傳遞現有 `MediaResource` 執行個體。

1. 至少檢查下列變更：

   * 已初始化
   * 已準備
   * 錯誤

     透過這些事件， `MediaPlayer` 物件可在媒體資源成功載入時通知應用程式。

1. 當媒體播放器的狀態變更為「已初始化」時，您可以呼叫 `MediaPlayer.prepareToPlay`

   INITIALIZED狀態表示媒體已成功載入。 通話 `prepareToPlay` 開始廣告解析度和刊登程式（如果有的話）。

1. 當媒體播放器狀態變更為「已準備」時，媒體串流已成功載入並準備播放。

   載入媒體資料流時， `MediaPlayerItem` 「 」已建立。

如果發生失敗，MediaPlayer會切換至ERROR狀態。 同時也會透過分派 `STATUS_CHANGED` 事件至您的 `MediaPlayerStatusChangeEvent` 回撥。

這會傳遞數個引數：
* A `type` 字串型別的引數，其值為 `ERROR`.

* A `MediaError` 可用來取得包含錯誤事件診斷資訊之通知的引數。


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

下列簡化的程式碼範例說明載入媒體資源的程式：

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```
