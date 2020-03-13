---
description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。
seo-description: 直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。
seo-title: 在MediaPlayer中載入媒體資源
title: 在MediaPlayer中載入媒體資源
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

直接執行個體化MediaResource並載入要播放的視訊內容，以載入資源。

1. 使用要 `MediaPlayer` 播放的新資源，設定物件的可播放項目。

   呼叫並傳 `MediaPlayer` 遞現有例項，以取代現有物 `replaceCurrentResource` 件的目前可播放 `MediaResource` 項目。

1. 等待瀏覽器TVSDK派 `AdobePSDK.MediaPlayerStatusChangeEvent` 單， `event.status` 其等於下列任一項：

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      透過這些事件，MediaPlayer物件會通知您的應用程式媒體資源是否已成功載入。

1. 當媒體播放器的狀態變更為時 `MediaPlayerStatus.INITIALIZED`，您可以呼叫 `MediaPlayer.prepareToPlay`。

   「已初始化」狀態表示介質已成功載入。 呼叫 `prepareToPlay` 會啟動廣告解析度和位置處理程式（如果有的話）。
1. 當瀏覽器TVSDK調度 `MediaPlayerStatus.PREPARED` 媒體串流已成功載入的事件（建立MediaPlayerItem）並準備播放。

如果發生故障，則 `MediaPlayer` 切換到 `MediaPlayerStatus.ERROR`。

此外，它還會傳送事件以通知您的應 `MediaPlayerStatus.ERROR` 用程式。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


以下簡化的范常式式碼說明載入媒體資源的程式：

>```js>
>player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
>                                               onStatusChange); 
> 
>
onStatusChange = function (event) { 
>       var msg = ""; 
>       switch (event.status) { 
>               case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
>                       msg = "Player Status: INITIALIZED"; 
>                       console.log(msg); 
>                       player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
>                       break; 
> 
>        
       case AdobePSDK.MediaPlayerStatus.PREPARED: 
>               // The resource is successfully loaded and available 
>               // and the MediaPlayer is ready to start the playback. 
>               // Once the resource is loaded, the MediaPlayer can 
>               // provide a reference to the current "playable item" 
>                     MediaPlayerItem playerItem = player.currentItem; 
>                     if (playerItem != null) {  
>                           // here we can look at the properties of the  
>                           // loadedstream 
>                     } 
>                     break; 
>       } 
>}
>```>


