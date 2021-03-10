---
description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。
title: 在MediaPlayer中載入媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# 在MediaPlayer中載入媒體資源{#load-a-media-resource-in-the-mediaplayer}

直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。

1. 使用要播放的新資源設定`MediaPlayer`對象的可播放項。

   呼叫`replaceCurrentResource`並傳遞現有的`MediaResource`例項，以取代您現有`MediaPlayer`物件目前可播放的項目。

1. 等待瀏覽器TVSDK將`AdobePSDK.MediaPlayerStatusChangeEvent`與`event.status`相等於下列任一項分派：

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      透過這些事件，MediaPlayer物件會通知您的應用程式媒體資源是否已成功載入。

1. 當媒體播放器的狀態變更為`MediaPlayerStatus.INITIALIZED`時，您可以呼叫`MediaPlayer.prepareToPlay`。

   「已初始化」狀態表示介質已成功載入。 呼叫`prepareToPlay`會啟動廣告解析度和位置處理程式（如果有的話）。
1. 當瀏覽器TVSDK派單`MediaPlayerStatus.PREPARED`事件時，媒體串流已成功載入（建立MediaPlayerItem）並準備播放。

如果發生故障， `MediaPlayer`將切換到`MediaPlayerStatus.ERROR`。

它還通過調度`MediaPlayerStatus.ERROR`事件來通知您的應用程式。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


以下簡化的范常式式碼說明載入媒體資源的程式：

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
