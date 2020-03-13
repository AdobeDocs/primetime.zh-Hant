---
description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。
seo-description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。
seo-title: 在媒體播放器中載入媒體資源
title: 在媒體播放器中載入媒體資源
uuid: 0334fa69-1d92-44d8-8891-2bc90a1ea498
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 在媒體播放器中載入媒體資源 {#load-a-media-resource-in-the-media-player}

直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。

1. 設定媒體播放器以播放新資源。

   呼叫並傳遞現有例項，以取代 `MediaPlayer.replaceCurrentResource()` 目前可播放的 `MediaResource` 項目。

   這將啟動資源載入進程。

1. 向實例 `MediaPlayerEvent.STATUS_CHANGED` 註冊事 `MediaPlayer` 件。 在回呼中，請至少檢查下列狀態值：

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`
   透過這些事件， `MediaPlayer` 物件會在成功載入媒體資源時通知您的應用程式。
1. 當媒體播放器的狀態變更為時 `INITIALIZED`，您可以呼叫 `MediaPlayer.prepareToPlay()`。

   此狀態表示介質已成功載入。 新功能 `MediaPlayerItem` 已可供播放。 呼叫 `prepareToPlay()` 會啟動廣告解析度和位置處理程式（如果有的話）。

如果發生故障，媒體播放器會切換至狀 `ERROR` 態。

以下簡化的范常式式碼說明載入媒體資源的程式：
>```java>
>// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
 new StatusChangeEventListener() { 
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
           // The resource is successfully loaded and available. The  
           // MediaPlayer is ready to start the playback and can 
           // provide a reference to the current playable item 
           MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
           if (playerItem != null) { 
               // We can look at the properties of the loaded stream 
           } 
       } 
       else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
           //Something bad happened - the resource cannot be loaded. 
           // The Metadata object in the event provides details. 
       } 
       else if (status == MediaPlayerStatus.INITIALIZED) { 
           mediaPlayer.prepareToPlay(); 
       } 
   } 
} 
```
