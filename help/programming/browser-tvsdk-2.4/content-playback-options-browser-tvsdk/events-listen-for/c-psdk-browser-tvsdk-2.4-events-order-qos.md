---
description: 瀏覽器TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝和查找事件。
title: QoS事件
exl-id: b0fab68e-ef0f-4812-b4ad-3f69dcdf2d9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# QoS事件{#qos-events}

瀏覽器TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝和查找事件。

要獲得有關所有QoS相關事件的通知，請建立 `AdobePSDK.QOSProvider` 並將MediaPlayer實例附加到此 `QOSProvider` 實例：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

配置應用程式中的計時器以定期檢查 `playbackInformation` 屬性 `qosProvider` 實例。 的 `playbackInformation` 屬性提供當前播放統計資訊的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
