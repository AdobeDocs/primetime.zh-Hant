---
description: 服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 瀏覽器TVSDK提供有關播放、緩衝和設備的詳細統計資訊。
title: 服務質量統計
exl-id: b7486ed5-e59f-428c-942c-a2fee7a869c9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 服務質量統計{#quality-of-service-statistics}

服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 瀏覽器TVSDK提供有關播放、緩衝和設備的詳細統計資訊。

## 讀取QOS回放、緩衝和設備統計資訊 {#read-qos-playback-buffering-and-device-statistics}

可以從QOSProvider類讀取回放、緩衝和設備統計資訊。

的 `QOSProvider` 類提供各種統計資訊，包括有關緩衝、比特率、幀速率、時間資料等的資訊。

1. 實例化媒體播放器。
1. 建立 `QOSProvider` 對象，並將其附加到媒體播放器。

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. （可選）閱讀回放統計資訊。

   讀取回放統計資訊的一個解決方案是具有計時器，該計時器定期從 `QOSProvider`。 例如：

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. （可選）讀取設備特定資訊。

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
