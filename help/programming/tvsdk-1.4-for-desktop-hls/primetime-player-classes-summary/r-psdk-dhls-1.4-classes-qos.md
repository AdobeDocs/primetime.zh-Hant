---
description: 這些類別提供的資訊可協助您判斷播放器是否表現良好。
title: QoS類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# QoS類別 {#qos-classes}

這些類別提供的資訊可協助您判斷播放器是否表現良好。

封裝： [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/package-detail.html)  封裝： [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> 緩衝量度</a></span> </td> 
   <td colname="2"> 提供有關播放器緩衝花費的時間以及緩衝事件發生頻率的資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> 裝置資訊</a></span> </td> 
   <td colname="2">提供TVSDK執行所在平台和作業系統的相關資訊： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台作業系統的版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">TVSDK程式庫的版本號碼 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">裝置的型號名稱 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">裝置製造商名稱 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">裝置UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">裝置熒幕的寬度/高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> 載入資訊</a></span> </td> 
   <td colname="2"> 包含載入各種資源（檔案、資訊清單或播放清單、片段/區段、曲目等）的各種QoS資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInfoType</a></span> </td> 
   <td colname="2"> 列示LoadInformation物件type屬性的可能值的列舉類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 播放資訊</a></span> </td> 
   <td colname="2"> 提供播放執行方式的資訊。 這包括影格速率、設定檔位元速率、緩衝所花費的總時間、緩衝嘗試次數、從第一個視訊片段取得第一個位元組所花費的時間、轉譯第一個影格所花費的時間、目前緩衝的長度以及緩衝時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 提供載入媒體所花時間、播放器轉譯第一個影格或失敗（發生錯誤）所花時間的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> 播放量度</a></span> </td> 
   <td colname="2"> 提供播放行為的相關資訊。 這包括影格速率、位元速率、緩衝區長度等。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> 提供播放器實際播放花費的秒數，以及視訊實際在熒幕上的時間等資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span> </td> 
   <td colname="2">
    <pre>
      為播放和裝置提供基本的QoS量度。
    </pre>
    <pre>
      QOS資訊提供者類別。
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
