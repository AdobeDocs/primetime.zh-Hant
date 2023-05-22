---
description: 通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。 這是載入媒體資源的一種方法。
title: 在媒體播放器中載入媒體資源
exl-id: f39d3aa2-8912-4dac-9f10-91b6d20395ea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 在媒體播放器中載入媒體資源 {#load-a-media-resource-in-the-media-player}

通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。 這是載入媒體資源的一種方法。

1. 設定媒體播放器以播放新資源。

   通過調用替換當前可播放項 `MediaPlayer.replaceCurrentResource()` 通過現有 `MediaResource` 實例。

   這將啟動資源載入進程。

1. 註冊 `MediaPlayerEvent.STATUS_CHANGED` 事件 `MediaPlayer` 實例。 在回調中，至少檢查以下狀態值：

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   通過這些活動， `MediaPlayer` 當應用程式成功載入媒體資源時，對象會通知它。
1. 當媒體播放器的狀態更改為 `INITIALIZED`您可以 `MediaPlayer.prepareToPlay()`。

   此狀態表示介質已成功載入。 新 `MediaPlayerItem` 已準備好播放。 呼叫 `prepareToPlay()` 啟動廣告解決和投放過程（如果有）。

如果出現故障，媒體播放器將切換到 `ERROR` 狀態。

以下簡化示例代碼說明了載入媒體資源的過程：

```java>
// mediaResource is a properly configured MediaResource instance 
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
