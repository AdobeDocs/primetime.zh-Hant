---
description: 透過直接例項化MediaResource並載入要播放的視訊內容來載入資源。
title: 在MediaPlayer中載入媒體資源
exl-id: b775c33e-399c-4a03-a132-407944f07706
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

透過直接例項化MediaResource並載入要播放的視訊內容來載入資源。

1. 設定您的 `MediaPlayer` 物件的可播放專案，以及要播放的新資源。

   取代您現有的 `MediaPlayer` 物件目前可播放的專案，方法是呼叫 `replaceCurrentResource` 並傳遞現有 `MediaResource` 執行個體。

1. 等待瀏覽器TVSDK派遣 `AdobePSDK.MediaPlayerStatusChangeEvent` 替換為 `event.status` 這等於下列任一專案：

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      透過這些事件，MediaPlayer物件會通知您的應用程式媒體資源是否已成功載入。

1. 當媒體播放器的狀態變更為 `MediaPlayerStatus.INITIALIZED`，您可以呼叫 `MediaPlayer.prepareToPlay`.

   INITIALIZED狀態表示媒體已成功載入。 通話 `prepareToPlay` 開始廣告解析度和刊登版位程式（如果有的話）。
1. 瀏覽器TVSDK傳送時 `MediaPlayerStatus.PREPARED` 媒體串流已成功載入的事件（已建立MediaPlayerItem）並準備播放。

如果失敗， `MediaPlayer` 切換至 `MediaPlayerStatus.ERROR`.

此外，也會透過傳送電子郵件通知應用程式 `MediaPlayerStatus.ERROR` 事件。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

下列簡化的範常式式碼說明載入媒體資源的程式：

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
