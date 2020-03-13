---
description: 瀏覽器TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。
seo-description: 瀏覽器TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。
seo-title: QoS事件
title: QoS事件
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# QoS事件{#qos-events}

瀏覽器TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。

若要收到所有QoS相關事件的通知，請建立MediaPlayer例項， `AdobePSDK.QOSProvider` 並將此MediaPlayer例項附加至此 `QOSProvider` 例項：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

在應用程式中設定計時器，以定期檢查 `playbackInformation` 例項的屬 `qosProvider` 性。 該屬 `playbackInformation` 性提供當前回放統計資訊的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

