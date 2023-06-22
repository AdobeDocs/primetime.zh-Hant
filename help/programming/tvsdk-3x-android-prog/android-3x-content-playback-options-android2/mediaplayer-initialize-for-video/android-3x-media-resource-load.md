---
description: 透過直接例項化MediaResource並載入要播放的視訊內容來載入資源。 這是載入媒體資源的其中一種方式。
title: 在媒體播放器中載入媒體資源
exl-id: f39d3aa2-8912-4dac-9f10-91b6d20395ea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 在媒體播放器中載入媒體資源 {#load-a-media-resource-in-the-media-player}

透過直接例項化MediaResource並載入要播放的視訊內容來載入資源。 這是載入媒體資源的其中一種方式。

1. 設定媒體播放器以播放新資源。

   呼叫以取代目前可播放的專案 `MediaPlayer.replaceCurrentResource()` 並傳遞現有 `MediaResource` 執行個體。

   這會啟動資源載入程式。

1. 註冊 `MediaPlayerEvent.STATUS_CHANGED` 事件與 `MediaPlayer` 執行個體。 在回呼中，至少檢查下列狀態值：

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   透過這些事件， `MediaPlayer` 物件會在應用程式成功載入媒體資源時通知您。
1. 當媒體播放器的狀態變更為 `INITIALIZED`，您可以呼叫 `MediaPlayer.prepareToPlay()`.

   此狀態表示媒體已成功載入。 新 `MediaPlayerItem` 已準備好播放。 通話 `prepareToPlay()` 開始廣告解析度和刊登版位程式（如果有的話）。

如果發生失敗，媒體播放器會切換至 `ERROR` 狀態。

下列簡化的範常式式碼說明載入媒體資源的程式：

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
