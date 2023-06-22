---
description: 這些類別提供的資訊可協助您判斷播放器的執行狀況。
title: QoS類別
exl-id: 7d8b2bb2-491d-4c36-a6b3-8f91cf2304aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# QoS類別 {#qos-classes}

這些類別提供的資訊可協助您判斷播放器的執行狀況。

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
   <td colname="2"> 提供播放器緩衝時所花費的時間以及緩衝事件發生頻率的資訊。 </td> 
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
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> Loadinformation</a></span> </td> 
   <td colname="2"> 包含載入各種資源（檔案、資訊清單或播放清單、片段/區段、曲目等）的各種QoS資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInformationtype</a></span> </td> 
   <td colname="2"> 列舉LoadInformation物件的type屬性的可能值的列舉類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 播放資訊</a></span> </td> 
   <td colname="2"> 提供有關播放執行方式的資訊。 這包括影格速率、設定檔位元速率、緩衝花費的總時間、緩衝嘗試次數、從第一個視訊片段取得第一個位元組所花的時間、轉譯第一個影格所花的時間、目前緩衝的長度，以及緩衝時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 提供載入媒體所需的時間、播放器轉譯第一個影格所需的時間，或是發生錯誤時失敗的資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> Playbackmetrics</a></span> </td> 
   <td colname="2"> 提供播放行為的相關資訊。 這包括影格速率、位元速率、緩衝區長度等。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> 提供播放器實際播放所花費的秒數，以及視訊實際在熒幕上的時間長短。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProviser</a></span> </td> 
   <td colname="2">
    <pre>
      提供播放和裝置的基本QoS量度。
    </pre>
    <pre>
      QOS資訊提供者類別。
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
