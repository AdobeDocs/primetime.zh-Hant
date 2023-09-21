---
description: 直接將MediaResource實體化並載入要播放的視訊內容，以載入資源。
title: 在MediaPlayer中載入媒體資源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

直接將MediaResource實體化並載入要播放的視訊內容，以載入資源。

1. 設定您的 `MediaPlayer` 物件的可播放專案，以及要播放的新資源。

   取代您現有的 `MediaPlayer` 物件目前可播放的專案，方法是呼叫 `replaceCurrentResource` 並傳遞現有 `MediaResource` 執行個體。

1. 等待瀏覽器TVSDK派遣 `AdobePSDK.MediaPlayerStatusChangeEvent` 替換為 `event.status` 這等於下列任一專案：

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

     透過這些事件，MediaPlayer物件會通知您的應用程式媒體資源是否已成功載入。

1. 當媒體播放器的狀態變更為 `MediaPlayerStatus.INITIALIZED`，您可以呼叫 `MediaPlayer.prepareToPlay`.

   INITIALIZED狀態表示媒體已成功載入。 通話 `prepareToPlay` 開始廣告解析度和刊登程式（如果有的話）。
1. 瀏覽器TVSDK傳送時 `MediaPlayerStatus.PREPARED` 事件媒體串流已成功載入（已建立MediaPlayerItem）並準備播放。

如果發生失敗， `MediaPlayer` 切換至 `MediaPlayerStatus.ERROR`.

同時也會透過分派 `MediaPlayerStatus.ERROR` 事件。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

下列簡化的程式碼範例說明載入媒體資源的程式：

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
