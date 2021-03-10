---
description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。
title: 在MediaPlayer中載入媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# 在MediaPlayer中載入媒體資源{#load-a-media-resource-in-the-mediaplayer}

直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。

1. 使用要播放的新資源設定`MediaPlayer`對象的可播放項。

   呼叫`MediaPlayer.replaceCurrentResource`並傳遞現有的`MediaResource`例項，以取代您現有的MediaPlayer目前可播放的項目。

1. 請至少檢查下列變更：

   * 已初始化
   * 準備好
   * 錯誤

      通過這些事件，`MediaPlayer`對象可以在媒體資源成功載入時通知您的應用程式。

1. 當媒體播放器的狀態更改為「已初始化」時，您可以調用`MediaPlayer.prepareToPlay`

   「已初始化」狀態表示介質已成功載入。 呼叫`prepareToPlay`會啟動廣告解析度和位置處理程式（如果有的話）。

1. 當媒體播放器狀態變更為PREPARED時，媒體串流已成功載入並準備播放。

   載入媒體串流時，會建立`MediaPlayerItem`。

如果發生故障，MediaPlayer會切換至「錯誤」狀態。 它還會將`STATUS_CHANGED`事件分派到您的`MediaPlayerStatusChangeEvent`回呼，以通知您的應用程式。

這會傳遞數個參數：
* 類型字串的`type`參數，其值為`ERROR`。

* `MediaError`參數，您可用來取得包含錯誤事件診斷資訊的通知。


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

以下簡化的范常式式碼說明載入媒體資源的程式：

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
