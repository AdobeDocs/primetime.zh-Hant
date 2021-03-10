---
description: 服務質量(QoS)提供視訊引擎執行的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
title: 服務質量統計
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# 服務質量統計資料{#quality-of-service-statistics}

服務質量(QoS)提供視訊引擎執行的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列下載資源的相關資訊：

* 播放清單／資訊清單檔案
* 檔案片段
* 檔案的追蹤資訊

## 使用載入資訊{#section_4439D91E8EDC45588EF1D7BE25697350}在片段層級追蹤

您可以從`LoadInformation`類別讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。

1. 實作並註冊`MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`事件偵聽器。
1. 呼叫`event.getLoadInformation()`以讀取傳遞至回呼的`event`參數的相關資料。

   >[!NOTE]
   >
   >如需`LoadInformation`的詳細資訊，請參閱[2.7 for Android(Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API檔案。

## 讀取QOS回放、緩衝和設備統計資訊{#section_D21722600F324E67A9F06234D338B243}

您可以從`QOSProvider`類別讀取播放、緩衝和裝置統計資料。

`QOSProvider`類別提供各種統計資料，包括緩衝、位元速率、影格速率、時間資料等資訊。 此外，它也提供有關裝置的資訊，例如製造商、型號、作業系統、SDK版本、製造商的裝置ID和螢幕大小／密度。

1. 實例化媒體播放器。
1. 建立`QOSProvider`物件，並將它附加至媒體播放器。

   `QOSProvider`建構函式會擷取播放器內容，以便擷取裝置特定資訊。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可選）閱讀播放統計資料。

   讀取播放統計資訊的一個解決方案是具有計時器，該計時器定期從`QOSProvider`中讀取新的QoS值。

   例如：

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. （可選）閱讀裝置特定資訊。

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```

