---
description: 透過直接例項化MediaResource並載入要播放的視訊內容來載入資源。 這是載入媒體資源的其中一種方式。
title: 在MediaPlayer中載入媒體資源
exl-id: 2d5e95bc-3962-4356-b90f-e550066f7a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

透過直接例項化MediaResource並載入要播放的視訊內容來載入資源。 這是載入媒體資源的其中一種方式。

1. 使用要播放的新資源設定MediaPlayer的可播放專案。

   呼叫，取代您現有的MediaPlayer目前可播放的專案 `MediaPlayer.replaceCurrentItem` 並傳遞現有 `MediaResource` 執行個體。

1. 註冊實作 `MediaPlayer.PlaybackEventListener` 與的介面 `MediaPlayer` 執行個體。

   * `onPrepared`
   * `onStateChanged`，並檢查「已初始化」和「錯誤」。

1. 當媒體播放器的狀態變更為「已初始化」時，您可以呼叫 `MediaPlayer.prepareToPlay`

   INITIALIZED狀態表示媒體已成功載入。 通話 `prepareToPlay` 開始廣告解析度和刊登版位程式（如果有的話）。

1. 當TVSDK呼叫 `onPrepared` callback，媒體資料流已成功載入，並準備好播放。

   載入媒體資料流時， `MediaPlayerItem` 「 」已建立。

>如果失敗， `MediaPlayer` 切換至ERROR狀態。 此外，也會透過呼叫 `PlaybackEventListener.onStateChanged`callback。
>
>這會傳遞數個引數：
>* A `state` 引數型別 `MediaPlayer.PlayerState` ，其值為 `MediaPlayer.PlayerState.ERROR`.
>
>* A `notification` 引數型別 `MediaPlayerNotification` 包含有關錯誤事件的診斷資訊。


下列簡化的範常式式碼說明載入媒體資源的程式：

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
