---
description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。
seo-description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。
seo-title: 在MediaPlayer中載入媒體資源
title: 在MediaPlayer中載入媒體資源
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。 這是載入介質資源的一種方法。

1. 使用要播放的新資源設定MediaPlayer的可播放項目。

   呼叫並傳遞現有例項，以取代您現有MediaPlayer `MediaPlayer.replaceCurrentItem` 的目前可播放 `MediaResource` 項目。

1. 向實例註冊接 `MediaPlayer.PlaybackEventListener` 口的實 `MediaPlayer` 施。

   * `onPrepared`
   * `onStateChanged`，並檢查是否已初始化和錯誤。

1. 當媒體播放器的狀態變更為「已初始化」時，您可以呼叫 `MediaPlayer.prepareToPlay`

   「已初始化」狀態表示介質已成功載入。 呼叫 `prepareToPlay` 會啟動廣告解析度和位置處理程式（如果有的話）。
1. 當TVSDK呼叫回 `onPrepared` 呼時，媒體串流已成功載入並準備播放。

   載入媒體串流時，會建 `MediaPlayerItem` 立。
>如果發生故障，則切 `MediaPlayer` 換到「ERROR（錯誤）」狀態。 它也會呼叫您的回呼來通知您的應 `PlaybackEventListener.onStateChanged`用程式。
>
>這會傳遞數個參數：>
>* 類 `state` 型的參 `MediaPlayer.PlayerState` 數，其值為 `MediaPlayer.PlayerState.ERROR`。
   >
   >
* 包含 `notification` 錯誤事件 `MediaPlayerNotification` 診斷資訊的類型參數。


以下簡化的范常式式碼說明載入媒體資源的程式：

>```java>
>// mediaResource is a properly configured MediaResource instance 
>// mediaPlayer is a MediaPlayer instance 
>// register a PlaybackEventListener implementation with the MediaPlayer  
>instancemediaPlayer.addEventListener( 
>   MediaPlayer.Event.PLAYBACK, 
>   new MediaPlayer.PlaybackEventListener()) { 
>       @Overridepublic void onPrepared() { 
>               // at this point, the resource is successfully loaded and available 
>               // and the MediaPlayer is ready to start the playback 
>               // once the resource is loaded, the MediaPlayer is able to 
>               // provide a reference to the current "playable item" 
> 
>        
       MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
> 
>        
       if (playerItem != null) {     
>                       // here we can take a look at the properties of the     
>                       // loaded stream 
>               } 
>       } @Overridepublic void onStateChanged( 
>               MediaPlayer.PlayerState state,  
>               MediaPlayerNotification notification) { 
>               if (state == MediaPlayer.PlayerState.ERROR) { 
>                       // something bad happened - the resource cannot be loaded    
>                       // details about the problem are provided via the  
>                       // MediaPlayerNotification instance 
>               }  
>               elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
>                       mediaPlayer.prepareToPlay(); 
>               } 
>       } 
>       // implementation of the other methods in the PlaybackEventListener interface... 
>} 
>
>
```>


