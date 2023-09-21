---
description: 服務品質(QoS)可提供視訊引擎執行狀況的詳細檢視。 瀏覽器TVSDK提供有關播放、緩衝和裝置的詳細統計資料。
title: 服務品質統計資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 服務品質統計資料{#quality-of-service-statistics}

服務品質(QoS)可提供視訊引擎執行狀況的詳細檢視。 瀏覽器TVSDK提供有關播放、緩衝和裝置的詳細統計資料。

## 讀取QOS播放、緩衝和裝置統計資料 {#read-qos-playback-buffering-and-device-statistics}

您可以從QOSProvider類別讀取播放、緩衝和裝置統計資料。

此 `QOSProvider` class提供各種統計資料，包括有關緩衝、位元速率、影格速率、時間資料的資訊，等等。

1. 例項化媒體播放器。
1. 建立 `QOSProvider` 物件並將其附加至媒體播放器。

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. （選用）讀取播放統計資料。

   讀取播放統計資料的解決方案之一，是讓計時器定期從擷取新的QoS值 `QOSProvider`. 例如：

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

1. （選擇性）讀取裝置特定資訊。

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
