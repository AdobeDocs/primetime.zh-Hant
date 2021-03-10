---
description: 這些類別提供的資訊可協助您判斷播放器的效能。
title: QoS類
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# QoS類{#qos-classes}

這些類別提供的資訊可協助您判斷播放器的效能。

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">提供有關TVSDK執行之平台和作業系統的資訊： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台作業系統版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">TVSDK程式庫的版本號碼 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">設備的型號名稱 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">裝置製造商的名稱 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">設備UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">裝置螢幕的寬度／高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> 提供播放執行方式的相關資訊。 這包括影格速率、描述檔位元速率、緩衝的總花費時間、緩衝嘗試次數、從第一個視訊片段取得第一個位元組所花的時間、轉譯第一個影格所花的時間、目前緩衝的長度，以及緩衝時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      為播放和裝置提供基本的QoS度量。
    </pre>
    <pre>
      QOS資訊提供器類別。
    </pre> </td> 
  </tr> 
 </tbody> 
</table>

