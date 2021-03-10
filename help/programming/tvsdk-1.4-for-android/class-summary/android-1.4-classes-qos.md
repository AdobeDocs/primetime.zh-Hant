---
description: 這些類別提供的資訊可協助您判斷播放器的效能。
title: QoS類
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# QoS類{#qos-classes}

這些類別提供的資訊可協助您判斷播放器的效能。

套件：[com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html)套件：[com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> BufferingMetrics</a></span></td> 
   <td colname="2"> 提供有關播放器在緩衝期間所花費的時間，以及緩衝事件發生頻率的資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> 裝置資訊</a> </span></td> 
   <td colname="2">提供有關片語所在平台和作業系統的資訊
    執行： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台作業系統版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">片語庫的版本號 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">設備的型號名稱 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">裝置製造商的名稱 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">設備UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">裝置螢幕的寬度／高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> 包含有關載入各種資源（檔案、資訊清單或播放清單、片段／區段、追蹤等）的各種QoS資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 播放資訊</a></span> </td> 
   <td colname="2"> 提供播放執行方式的相關資訊。 這包括影格速率、描述檔位元速率、緩衝的總花費時間、緩衝嘗試次數、從第一個視訊片段取得第一個位元組所花的時間、轉譯第一個影格所花的時間、目前緩衝的長度，以及緩衝時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 提供媒體載入所花的時間、播放器轉換第一個影格所花的時間，或在發生錯誤時失敗的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> 播放量度</a> </span></td> 
   <td colname="2"> 提供播放行為的相關資訊。 這包括幀速率、位速率、緩衝長度等。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> 提供播放器實際播放所花費的秒數，以及視訊實際在螢幕上播放的時間等資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span></td> 
   <td colname="2">為播放和裝置提供基本的QoS度量。 QOS資訊提供器類別。</td> 
  </tr> 
 </tbody> 
</table>
