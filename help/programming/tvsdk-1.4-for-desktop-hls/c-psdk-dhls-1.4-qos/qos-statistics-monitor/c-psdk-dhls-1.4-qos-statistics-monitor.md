---
description: 服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。
title: 服務質量統計
exl-id: ab664d75-a24f-41d6-91d7-a26ad7baab9a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 服務質量統計 {#quality-of-service-statistics}

服務質量(QoS)提供視頻引擎如何運行的詳細視圖。 TVSDK提供有關播放、緩衝和設備的詳細統計資訊。

TVSDK還提供有關以下下載資源的資訊：

* 播放清單/清單檔案
* 檔案片段
* 檔案跟蹤資訊

## 使用負載資訊在片段級別跟蹤 {#track-at-the-fragment-level-using-load-information}

可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。

1. 實施 `onLoadInformationAvailable` 回調事件偵聽器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 註冊事件偵聽器，TVSDK每次下載片段時都會調用該偵聽器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 從 `LoadInformation` 傳給回叫的。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 屬性 </th> 
      <th colname="col1" class="entry"> 類型 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 下載持續時間 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> <p>下載的持續時間（毫秒）。 </p> <p>TVSDK不區分客戶端連接到伺服器所花的時間和下載完整片段所花的時間。 例如，如果10 MB的段下載需要8秒，則TVSDK會提供該資訊，但不會告訴您下載整個片段需要4秒，直到第一個位元組再花4秒。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 媒體持續時間 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 下載的片段的媒體持續時間（毫秒）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 已下載資源的大小（以位元組為單位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤索引 </span> </td> 
      <td colname="col1"> <p>整 </p> </td> 
      <td colname="col2"> 相應軌道的索引（如果已知）;否則，為0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤名稱 </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的名稱（如果已知）;否則，為空。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 跟蹤類型 </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的類型（如果已知）;否則，為空。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 類型 </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> TVSDK下載的內容。 以下情況之一： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST — 播放清單/清單 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENT — 片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK — 與特定跟蹤關聯的片段 </li> 
      </ul> 有時，可能無法檢測資源的類型。 如果發生這種情況，則返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 指向下載資源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>

## 讀取QOS回放、緩衝和設備統計資訊 {#read-qos-playback-buffering-and-device-statistics}

可以從QOSProvider類讀取回放、緩衝和設備統計資訊。

的 `QOSProvider` 類提供各種統計資訊，包括有關緩衝、比特率、幀速率、時間資料等的資訊。

它還提供有關設備的資訊，如製造商、型號、作業系統、SDK版本和螢幕大小/密度。

1. 實例化媒體播放器。
1. 建立 `QOSProvider` 對象，並將其附加到媒體播放器。

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可選）閱讀回放統計資訊。

   讀取回放統計資訊的一個解決方案是具有計時器，該計時器定期從 `QOSProvider`。 例如：

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. （可選）讀取設備特定資訊。

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```
