---
description: 瀏覽器TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝和搜尋事件。
title: QoS事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# QoS事件{#qos-events}

瀏覽器TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝和搜尋事件。

若要接收所有QoS相關事件的通知，請建立 `AdobePSDK.QOSProvider` 並將MediaPlayer例項附加至此 `QOSProvider` 例項：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

在應用程式中設定計時器，以定期檢查 `playbackInformation` 的屬性 `qosProvider` 執行個體。 此 `playbackInformation` 屬性提供目前播放統計資料的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
