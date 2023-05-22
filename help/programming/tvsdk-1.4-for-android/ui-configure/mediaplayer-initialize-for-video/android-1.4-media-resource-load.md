---
description: 通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。 這是載入媒體資源的一種方法。
title: 在MediaPlayer中載入媒體資源
exl-id: 2d5e95bc-3962-4356-b90f-e550066f7a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。 這是載入媒體資源的一種方法。

1. 將MediaPlayer的可播放項目與要播放的新資源一起設定。

   通過調用替換現有MediaPlayer的當前可播放項 `MediaPlayer.replaceCurrentItem` 通過現有 `MediaResource` 實例。

1. 註冊 `MediaPlayer.PlaybackEventListener` 與 `MediaPlayer` 實例。

   * `onPrepared`
   * `onStateChanged`，並檢查是否已初始化和錯誤。

1. 當媒體播放器的狀態更改為INITIALIZED時，可以調用 `MediaPlayer.prepareToPlay`

   INITIALIZED狀態表示媒體已成功載入。 呼叫 `prepareToPlay` 啟動廣告解決和投放過程（如果有）。

1. 當TVSDK調用 `onPrepared` 回調，媒體流已成功載入並準備播放。

   載入媒體流時， `MediaPlayerItem` 的子菜單。

>如果出現故障， `MediaPlayer` 切換到「ERROR（錯誤）」狀態。 它還通過調用 `PlaybackEventListener.onStateChanged`回叫。
>
>這會傳遞幾個參數：
>* A `state` 類型參數 `MediaPlayer.PlayerState` 值 `MediaPlayer.PlayerState.ERROR`。
>
>* A `notification` 類型參數 `MediaPlayerNotification` 包含有關錯誤事件的診斷資訊。


以下簡化示例代碼說明了載入媒體資源的過程：

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
