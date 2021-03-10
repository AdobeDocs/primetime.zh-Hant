---
description: 瀏覽器TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。
title: QoS事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# QoS事件{#qos-events}

瀏覽器TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。

要獲得所有QoS相關事件的通知，請建立`AdobePSDK.QOSProvider`實例，並將MediaPlayer實例附加到此`QOSProvider`實例：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

在應用程式中配置計時器以定期檢查`qosProvider`實例的`playbackInformation`屬性。 `playbackInformation`屬性提供當前回放統計資訊的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

