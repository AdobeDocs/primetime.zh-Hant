---
description: 通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。 這是載入媒體資源的一種方法。
title: 在MediaPlayer中載入媒體資源
exl-id: 8258c45e-f8bf-434d-9621-88c189e1530d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源{#load-a-media-resource-in-the-mediaplayer}

通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。 這是載入媒體資源的一種方法。

1. 設定 `MediaPlayer` 對象的可播放項，以及要播放的新資源。

   通過調用替換現有MediaPlayer的當前可播放項 `MediaPlayer.replaceCurrentResource` 通過現有 `MediaResource` 實例。

1. 至少檢查以下更改：

   * 已初始化
   * 準備
   * 錯誤

      通過這些活動， `MediaPlayer` 在成功載入媒體資源時，對象可以通知您的應用程式。

1. 當媒體播放器的狀態更改為INITIALIZED時，可以調用 `MediaPlayer.prepareToPlay`

   INITIALIZED狀態表示媒體已成功載入。 呼叫 `prepareToPlay` 啟動廣告解決和投放過程（如果有）。

1. 當媒體播放器狀態更改為PREPARED時，媒體流已成功載入並準備播放。

   載入媒體流時， `MediaPlayerItem` 的子菜單。

如果出現故障，MediaPlayer將切換到「ERROR（錯誤）」狀態。 它還通過調度 `STATUS_CHANGED` 事件 `MediaPlayerStatusChangeEvent` 回叫。

這會傳遞幾個參數：
* A `type` 帶值的字串類型參數 `ERROR`。

* A `MediaError` 參數，用於獲取包含有關錯誤事件的診斷資訊的通知。


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

以下簡化示例代碼說明了載入媒體資源的過程：

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
