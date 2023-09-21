---
description: 服務品質(QoS)可提供視訊引擎執行狀況的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
title: 服務品質統計資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 服務品質統計資料 {#quality-of-service-statistics}

服務品質(QoS)可提供視訊引擎執行狀況的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列已下載資源的相關資訊：

* 播放清單/資訊清單檔案
* 檔案片段
* 檔案的追蹤資訊

## 使用載入資訊在片段層級追蹤 {#section_4439D91E8EDC45588EF1D7BE25697350}

您可以閱讀服務品質(QoS)資訊，瞭解下載的資源，例如片段和曲目，網址為 `LoadInformation` 類別。

1. 實作並註冊 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 事件監聽器。
1. 呼叫 `event.getLoadInformation()` 以從讀取相關資料 `event` 傳遞至回呼的引數。

   >[!NOTE]
   >
   >深入瞭解 `LoadInformation`，請參閱 [Android適用的3.0 (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html) API檔案。

## 讀取QOS播放、緩衝和裝置統計資料 {#section_D21722600F324E67A9F06234D338B243}

您可以讀取播放、緩衝和裝置統計資料，從 `QOSProvider` 類別。

此 `QOSProvider` class提供各種統計資料，包括有關緩衝、位元速率、影格速率、時間資料的資訊，等等。 也會提供裝置的相關資訊，例如製造商、型號、作業系統、SDK版本、製造商的裝置ID以及熒幕大小/密度。

1. 例項化媒體播放器。
1. 建立 `QOSProvider` 物件並將其附加至媒體播放器。

   此 `QOSProvider` 建構函式會擷取播放器內容，以便擷取裝置特定資訊。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （選用）讀取播放統計資料。

   讀取播放統計資料的解決方案之一，是讓計時器定期從擷取新的QoS值 `QOSProvider`.

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

1. （選擇性）讀取裝置特定資訊。

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
