---
description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。
title: 在MediaPlayer中載入媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# 在MediaPlayer中載入媒體資源{#load-a-media-resource-in-the-mediaplayer}

直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。

1. 使用要播放的新資源設定MediaPlayer的可播放項目。

   呼叫`MediaPlayer.replaceCurrentItem`並傳遞現有的`MediaResource`例項，以取代您現有的MediaPlayer目前可播放的項目。

1. 向`MediaPlayer`實例註冊`MediaPlayer.PlaybackEventListener`介面的實現。

   * `onPrepared`
   * `onStateChanged`，並檢查是否已初始化和錯誤。

1. 當媒體播放器的狀態更改為「已初始化」時，您可以調用`MediaPlayer.prepareToPlay`

   「已初始化」狀態表示介質已成功載入。 呼叫`prepareToPlay`會啟動廣告解析度和位置處理程式（如果有的話）。

1. 當TVSDK呼叫`onPrepared`回呼時，媒體串流已成功載入並已準備好播放。

   載入媒體串流時，會建立`MediaPlayerItem`。

>如果發生故障， `MediaPlayer`將切換到ERROR狀態。 它也會呼叫您的`PlaybackEventListener.onStateChanged`回呼來通知您的應用程式。
>
>這會傳遞數個參數：
>* 類型`MediaPlayer.PlayerState`的`state`參數，其值為`MediaPlayer.PlayerState.ERROR`。
   >
   >
* 類型`MediaPlayerNotification`的`notification`參數，包含有關錯誤事件的診斷資訊。


以下簡化的范常式式碼說明載入媒體資源的程式：

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```
