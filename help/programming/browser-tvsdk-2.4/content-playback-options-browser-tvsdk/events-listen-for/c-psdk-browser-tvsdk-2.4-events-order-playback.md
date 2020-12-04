---
description: 瀏覽器TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。
seo-description: 瀏覽器TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。
seo-title: 播放事件的順序
title: 播放事件的順序
uuid: 259a9a2d-3d28-4240-b392-cc81f5c3f0cf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 播放事件的順序{#order-of-playback-events}

瀏覽器TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

下列範例顯示包含播放事件的某些事件的順序。

* 通過`replaceCurrentResource`成功載入媒體資源時，事件順序為：

   * `AdobePSDK.MediaPlayerStatusChangeEvent` with  `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* 當透過`MediaPlayer.prepareToPlay`準備播放時，事件的順序為：

   * `AdobePSDK.MediaPlayerStatusChangeEvent` with  `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

下列範例顯示事件的典型進展：

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```

