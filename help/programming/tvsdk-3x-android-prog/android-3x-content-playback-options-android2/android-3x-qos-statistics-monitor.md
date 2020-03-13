---
description: 服務質量(QoS)提供視訊引擎執行的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
seo-description: 服務質量(QoS)提供視訊引擎執行的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
seo-title: 服務質量統計
title: 服務質量統計
uuid: 3d66ed44-9d4a-4162-962f-e238575ff2dd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 服務質量統計 {#quality-of-service-statistics}

服務質量(QoS)提供視訊引擎執行的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列下載資源的相關資訊：

* 播放清單／資訊清單檔案
* 檔案片段
* 檔案的追蹤資訊

## 使用載入資訊在片段層級追蹤 {#section_4439D91E8EDC45588EF1D7BE25697350}

您可以從類別中讀取有關下載資源（例如片段和追蹤）的服務品質(QoS) `LoadInformation` 資訊。

1. 實作和註冊事 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 件偵聽器。
1. 呼 `event.getLoadInformation()` 叫以從傳遞至回呼的參 `event` 數讀取相關資料。

   >[!NOTE]
   >
   >如需詳細 `LoadInformation`資訊， [請參閱Android(Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html) API檔案的3.0。

## 讀取QOS播放、緩衝和設備統計資訊 {#section_D21722600F324E67A9F06234D338B243}

您可以從類別中讀取播放、緩衝和裝置統計 `QOSProvider` 資料。

該類 `QOSProvider` 別提供各種統計資料，包括緩衝、位元速率、影格速率、時間資料等資訊。 此外，它也提供有關裝置的資訊，例如製造商、型號、作業系統、SDK版本、製造商的裝置ID和螢幕大小／密度。

1. 實例化媒體播放器。
1. 建立物 `QOSProvider` 件並附加至媒體播放器。

   建構 `QOSProvider` 函式會擷取播放器內容，以便擷取裝置特定的資訊。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可選）閱讀播放統計資料。

   讀取播放統計資訊的一個解決方案是具有計時器，該計時器定期從中讀取新的QoS值 `QOSProvider`。

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
