---
description: 服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。
title: 服務質量統計
exl-id: 084b5aa7-1eea-464b-a425-1da7b9fa1731
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 服務質量統計 {#quality-of-service-statistics}

服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。

TVSDK還提供有關以下下載資源的資訊：

* 播放清單/清單檔案
* 檔案片段
* 檔案跟蹤資訊

## 使用負載資訊在片段級別跟蹤 {#section_4439D91E8EDC45588EF1D7BE25697350}

您可以從以下位置讀取有關下載資源（如碎片和軌道）的服務質量(QoS)資訊： `LoadInformation` 類。

1. 實施和註冊 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 事件偵聽器。
1. 呼叫 `event.getLoadInformation()` 從 `event` 傳遞給回調的參數。

   >[!NOTE]
   >
   >有關 `LoadInformation`，請參閱 [2.7適用於Android(Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API文檔。

## 讀取QOS回放、緩衝和設備統計資訊 {#section_D21722600F324E67A9F06234D338B243}

可以從 `QOSProvider` 類。

的 `QOSProvider` 類提供各種統計資訊，包括有關緩衝、比特率、幀速率、時間資料等的資訊。 它還提供有關設備的資訊，如製造商、型號、作業系統、SDK版本、製造商的設備ID和螢幕大小/密度。

1. 實例化媒體播放器。
1. 建立 `QOSProvider` 對象，並將其附加到媒體播放器。

   的 `QOSProvider` 建構子採用播放器上下文以便能夠檢索設備特定的資訊。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可選）閱讀回放統計資訊。

   讀取回放統計資訊的一個解決方案是具有計時器，該計時器定期從 `QOSProvider`。

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

1. （可選）讀取設備特定資訊。

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
