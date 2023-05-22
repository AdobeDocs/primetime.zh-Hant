---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: 用於訪問媒體資源資訊的媒體播放器方法
exl-id: 74e453d6-233e-4146-9f63-ab6919a4ba39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 用於訪問媒體資源資訊的媒體播放器方法{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>即時流 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isLive():Boolean; </span> </td> 
   <td colname="3"> <p>如果流是活的，則為true;如果為VOD，則為false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>受DRM保護</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isProtected():Boolean; </span> </td> 
   <td colname="3"> <p>如果流受DRM保護，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get drmMetadataInfos():向量圖。&lt;drmmetadatainfo&gt;; </span> </td> 
   <td colname="3"> <p>列出清單中發現的所有DRM元資料對象。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隱藏字幕</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasClosedCaptions():Boolean; </span> </td> 
   <td colname="3"> <p>如果隱藏字幕磁軌可用，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get closedCaptionsTracks():Vector。&lt;closedcaptionstrack&gt;; </span> </td> 
   <td colname="3"> <p>提供可用的隱藏字幕軌道清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get selectedClosedCaptionsTrack():ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>檢索當前所選的隱藏字幕 <span class="codeph"> SelectClosedCaptionsTrack </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptonsTrack(closedCaptontsTrack:com.adobe.mediacore.info:ClosedCaptionsTrack) </span> </td> 
   <td colname="3"> <p>將隱藏字幕軌道設定為當前隱藏字幕軌道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>備用音頻軌道 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasAlternateAudio():Boolean; </span> </td> 
   <td colname="3"> <p>如果流具有備用音頻軌道，則為True。 </p> <p>提示：主音軌（預設）也是備用音軌清單的一部分。 </p> <p>Desktop HLS的TVSDK認為主音頻跟蹤是備用音頻跟蹤清單中的項之一。 因此，唯一一個 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 返回false時，流根本沒有音頻。 如果內容只有一個音頻軌道，則此方法返回true, <span class="codeph"> 獲取音頻軌道 </span> 返回包含單個元素（預設音頻軌道）的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get audioTracks():Vector。&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> 提供可用備用音頻軌道的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get audioTracks():Vector。&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> <p>提供可用備用音頻軌道的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get selectedAudioTrack():AudioTrack; </span> </td> 
   <td colname="3"> <p>檢索所選的音頻軌道 <span class="codeph"> 選擇音頻軌道 </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack:AudioTrack) </span> </td> 
   <td colname="3"> <p>選擇要成為當前音頻軌道的音頻軌道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定時元資料</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasTimedMetadata():Boolean; </span> </td> 
   <td colname="3"> <p>如果流已關聯定時元資料，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get timedMetadata():Vector。&lt;timedmetadata&gt;; </span> </td> 
   <td colname="3"> <p>提供與流關聯的定時元資料對象的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isDynamic():Boolean; </span> </td> 
   <td colname="3"> <p>如果流是多比特率(MBR)流，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get profiles():Vector。&lt;profile&gt;; </span> </td> 
   <td colname="3"> <p>提供關聯比特率配置檔案的清單。 對於每個輪廓，可檢索其位速率以及輪廓的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>戲法 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isTrickPlaySupported():Boolean; </span> </td> 
   <td colname="3"> <p>如果玩家支援快速前進、倒帶和恢復，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get availablePlaybackRates():Vector。&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>提供特技播放功能上下文中可用播放速率的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體播放器 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get player():MediaPlayer </span> </td> 
   <td colname="3"> <p>返回當前與此播放器關聯的媒體播放器。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體資源</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get resource():MediaResource; </span> </td> 
   <td colname="3"> <p>返回與此項關聯的媒體資源。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> 函式獲取resourceId():int </span> </td> 
   <td colname="3"> <p>返回與此項關聯的媒體標識符。 </p> </td> 
  </tr> 
 </tbody> 
</table>
