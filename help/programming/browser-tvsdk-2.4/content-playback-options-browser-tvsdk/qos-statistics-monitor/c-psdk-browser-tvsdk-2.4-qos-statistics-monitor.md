---
description: 服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 瀏覽器TVSDK提供播放、緩衝和裝置的詳細統計資料。
seo-description: 服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 瀏覽器TVSDK提供播放、緩衝和裝置的詳細統計資料。
seo-title: 服務質量統計
title: 服務質量統計
uuid: e4bb2617-d8a7-4da7-b669-d6ffab2864bb
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 服務質量統計{#quality-of-service-statistics}

服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 瀏覽器TVSDK提供播放、緩衝和裝置的詳細統計資料。

## 讀取QOS播放、緩衝和設備統計資訊 {#read-qos-playback-buffering-and-device-statistics}

您可以從QOSProvider類讀取播放、緩衝和設備統計資訊。

該類 `QOSProvider` 別提供各種統計資料，包括緩衝、位元速率、影格速率、時間資料等資訊。

1. 實例化媒體播放器。
1. 建立物 `QOSProvider` 件並附加至媒體播放器。

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. （可選）閱讀播放統計資料。

   讀取播放統計資訊的一個解決方案是具有計時器，該計時器定期從中讀取新的QoS值 `QOSProvider`。 例如：

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

1. （可選）閱讀裝置特定資訊。

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
