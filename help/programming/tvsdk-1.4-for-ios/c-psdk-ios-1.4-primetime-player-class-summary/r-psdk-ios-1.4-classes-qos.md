---
description: 這些類提供資訊，幫助您確定播放器的效能。
title: QoS類
exl-id: ba0cddd0-3af9-4e35-9079-97c260cbd3e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# QoS類{#qos-classes}

這些類提供資訊，幫助您確定播放器的效能。

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDevice資訊</a> </td> 
   <td colname="2">提供有關TVSDK運行的平台和作業系統的資訊： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台OS的版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">TVSDK庫的版本號 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">設備的型號名稱 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">設備製造商的名稱 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">設備UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">設備螢幕的寬度/高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlayback資訊</a> </td> 
   <td colname="2"> 提供有關播放的執行方式的資訊。 這包括幀速率、配置檔案比特率、在緩衝中花費的總時間、緩衝嘗試次數、從第一視頻片段獲取第一位元組所花的時間、呈現第一幀所花的時間、當前緩衝的長度和緩衝時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      為播放和設備提供基本的QoS指標。
    </pre>
    <pre>
      QOS資訊提供程式類。
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
