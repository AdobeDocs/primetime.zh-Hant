---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: 用於訪問媒體資源資訊的媒體播放器方法
exl-id: 8849411a-e94b-43a9-9fa1-143725264304
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '405'
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
   <td colname="1"> <b>廣告標籤</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> <p>提供用於廣告放置過程的廣告標籤清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>即時流</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive(); </span> </td> 
   <td colname="3"> <p>如果流是活的，則為true;如果為VOD，則為false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>受DRM保護</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected(); </span> </td> 
   <td colname="3"> <p>如果流受DRM保護，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;drmmetadatainfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> <p>列出清單中發現的所有DRM元資料對象。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隱藏字幕</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布爾型hasClosedCaptions(); </span> </td> 
   <td colname="3"> <p>如果隱藏字幕磁軌可用，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;closedcaptionstrack&gt; getClosedActionsTracks(); </span> </td> 
   <td colname="3"> <p>提供可用的隱藏字幕軌道清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack獲取SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> <p>檢索當前所選的隱藏字幕 <span class="codeph"> SelectClosedCaptionsTrack </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> <p>將隱藏字幕軌道設定為當前隱藏字幕軌道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>備用音頻軌道</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布爾型hasAlternateAudio(); </span> </td> 
   <td colname="3"> <p>如果流具有備用音頻軌道，則為True。 </p> <p>提示：主音軌（預設）也是備用音軌清單的一部分。 </p> <p>用於Android的TVSDK認為主音頻軌道是備用音頻軌道清單中的項目之一。 因此，唯一一個 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 返回false時，流根本沒有音頻。 如果內容只有一個音頻軌道，則此方法返回true, <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 返回包含單個元素（預設音頻軌道）的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> 提供可用備用音頻軌道的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> <p>提供可用備用音頻軌道的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> <p>檢索所選的音頻軌道 <span class="codeph"> 選擇音頻軌道 </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 選擇AudioTrack(AudioTrack audioTrack) </span> </td> 
   <td colname="3"> <p>選擇要成為當前音頻軌道的音頻軌道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定時元資料</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布爾型hasTimedMetadata(); </span> </td> 
   <td colname="3"> <p>如果流已關聯定時元資料，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> <p>提供與流關聯的定時元資料對象的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic(); </span> </td> 
   <td colname="3"> <p>如果流是多比特率(MBR)流，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> <p>提供關聯比特率配置檔案的清單。 對於每個輪廓，可檢索其位速率以及輪廓的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>戲法</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported(); </span> </td> 
   <td colname="3"> <p>如果玩家支援快速前進、倒帶和恢復，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;浮點&gt; getAvailablePlaybackRates </span> </td> 
   <td colname="3"> <p>提供特技播放功能上下文中可用播放速率的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體資源</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> <p>返回與此項關聯的媒體資源。 </p> </td> 
  </tr> 
 </tbody> 
</table>
