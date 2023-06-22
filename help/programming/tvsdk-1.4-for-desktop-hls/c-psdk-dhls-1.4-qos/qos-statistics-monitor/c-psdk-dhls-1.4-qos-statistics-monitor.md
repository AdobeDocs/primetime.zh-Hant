---
description: 服務品質(QoS)提供視訊引擎執行狀況的詳細檢視。 TVSDK提供有關播放、緩衝和裝置的詳細統計資料。
title: 服務品質統計資料
exl-id: ab664d75-a24f-41d6-91d7-a26ad7baab9a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 服務品質統計資料 {#quality-of-service-statistics}

服務品質(QoS)提供視訊引擎執行狀況的詳細檢視。 TVSDK提供有關播放、緩衝和裝置的詳細統計資料。

TVSDK也提供下列已下載資源的相關資訊：

* 播放清單/資訊清單檔案
* 檔案片段
* 檔案的追蹤資訊

## 使用載入資訊在片段層級追蹤 {#track-at-the-fragment-level-using-load-information}

您可以從LoadInformation類別讀取有關已下載資源（例如片段和曲目）的服務品質(QoS)資訊。

1. 實作 `onLoadInformationAvailable` 回呼事件監聽器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 註冊事件監聽器，TVSDK在每次下載片段時都會呼叫此監聽器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 從讀取感興趣的資料 `LoadInformation` 會傳遞至回撥的專案。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 屬性 </th> 
      <th colname="col1" class="entry"> 型別 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadduration </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> <p>下載持續時間（毫秒）。 </p> <p>TVSDK不會區分使用者端連線至伺服器所花的時間與下載完整片段所花的時間。 例如，如果下載10 MB的區段需要8秒，TVSDK會提供該資訊，但不會告訴您直到第一個位元組花了4秒，然後又花了4秒來下載整個片段。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 下載片段的媒體持續時間（毫秒）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <p>數字 </p> </td> 
      <td colname="col2"> 已下載資源的大小（位元組）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 對應曲目的索引（如果已知）；否則為0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 對應曲目的名稱（如果已知）；否則為null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 對應曲目的型別（如果已知）；否則為null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 下載的TVSDK。 下列其中一項： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">資訊清單 — 播放清單/資訊清單 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段 — 片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK — 與特定曲目相關聯的片段 </li> 
      </ul> 有時可能無法偵測資源的型別。 如果發生此情況，則會傳回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>字串 </p> </td> 
      <td colname="col2"> 指向已下載資源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>

## 讀取QOS播放、緩衝和裝置統計資料 {#read-qos-playback-buffering-and-device-statistics}

您可以從QOSProvider類別讀取播放、緩衝和裝置統計資料。

此 `QOSProvider` class提供各種統計資料，包括關於緩衝、位元速率、影格速率、時間資料等的資訊。

此外也提供裝置的相關資訊，例如製造商、型號、作業系統、SDK版本和熒幕大小/密度。

1. 例項化媒體播放器。
1. 建立 `QOSProvider` 物件並將其附加至媒體播放器。

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （選用）讀取播放統計資料。

   讀取播放統計資料的解決方案之一，是讓計時器定期從擷取新的QoS值 `QOSProvider`. 例如：

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

1. （選擇性）讀取裝置特定資訊。

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
