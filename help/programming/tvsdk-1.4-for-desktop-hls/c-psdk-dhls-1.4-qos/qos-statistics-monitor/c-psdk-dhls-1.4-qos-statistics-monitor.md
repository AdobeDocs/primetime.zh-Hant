---
description: 服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。
title: 服務質量統計
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 服務質量統計資料{#quality-of-service-statistics}

服務品質(QoS)提供視訊引擎執行情形的詳細檢視。 TVSDK提供播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列下載資源的相關資訊：

* 播放清單／資訊清單檔案
* 檔案片段
* 檔案的追蹤資訊

## 使用載入資訊{#track-at-the-fragment-level-using-load-information}在片段層級追蹤

您可以從LoadInformation類讀取有關下載資源（如片段和軌道）的服務質量(QoS)資訊。

1. 實作`onLoadInformationAvailable`回呼事件偵聽器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 註冊事件偵聽器，TVSDK會在每次片段下載時呼叫該偵聽器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 讀取傳遞至回呼的`LoadInformation`中的相關資料。

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
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> <p>下載的持續時間（以毫秒為單位）。 </p> <p>TVSDK不會區分用戶端連線至伺服器的時間與下載完整片段所花的時間。 例如，如果10 MB區段需要8秒才能下載，TVSDK會提供該資訊，但不會告訴您直到第一個位元組再下載4秒，才下載整個片段。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 下載片段的媒體持續時間（以毫秒為單位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小  </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 已下載資源的大小（以位元組為單位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 相應軌道的索引（如果已知）;否則，為0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的名稱（如果已知）;否則，為null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 相應軌道的類型（如果已知）;否則，為null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> TVSDK下載的內容。 下列其中一項： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST —— 播放清單／資訊清單 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段——片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK —— 與特定軌道關聯的片段 </li> 
      </ul> 有時可能無法檢測資源類型。 如果發生這種情況，則返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 指向已下載資源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>

## 讀取QOS回放、緩衝和設備統計資訊{#read-qos-playback-buffering-and-device-statistics}

您可以從QOSProvider類讀取播放、緩衝和設備統計資訊。

`QOSProvider`類別提供各種統計資料，包括緩衝、位元速率、影格速率、時間資料等資訊。

此外，它還提供有關裝置的資訊，例如製造商、機型、作業系統、SDK版本和螢幕大小／密度。

1. 實例化媒體播放器。
1. 建立`QOSProvider`物件，並將它附加至媒體播放器。

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可選）閱讀播放統計資料。

   讀取播放統計資訊的一個解決方案是具有計時器，該計時器定期從`QOSProvider`中讀取新的QoS值。 例如：

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

1. （可選）閱讀裝置特定資訊。

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
