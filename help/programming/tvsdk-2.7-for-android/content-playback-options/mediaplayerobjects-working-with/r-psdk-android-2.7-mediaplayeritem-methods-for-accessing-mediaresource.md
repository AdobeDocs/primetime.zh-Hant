---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: MediaPlayerItem存取MediaResource資訊的方法
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# 用於訪問MediaResource資訊{#mediaplayeritem-methods-for-accessing-mediaresource-information}的MediaPlayerItem方法

MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>廣告標籤</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> 提供用於廣告放置程式的廣告標籤清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>即時串流</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive();  </span> </td> 
   <td colname="3"> 如果串流是即時的，則為true;false（如果是VOD）。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>受DRM保護</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected();  </span> </td> 
   <td colname="3"> 如果流受DRM保護，則為true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> 列出在資訊清單中發現的所有DRM中繼資料物件。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>隱藏字幕</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions();  </span> </td> 
   <td colname="3"> 如果隱藏字幕音軌可用，則為true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedActionsTracks();  </span> </td> 
   <td colname="3"> 提供可用隱藏字幕音軌的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack獲取SelectedClosedCaptionsTrack();  </span> </td> 
   <td colname="3"> 擷取使用<span class="codeph"> SelectClosedCaptionsTrack </span>選取的目前隱藏字幕軌道。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> 將隱藏字幕軌道設定為當前隱藏字幕軌道。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>替代音軌</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasAlternateAudio();  </span> </td> 
   <td colname="3"> 如果串流有替代的音軌，則為true。 <p>注意： 主音軌（預設）也是替代音軌清單的一部分。 </p> <p>適用於Android的TVSDK會將主要音軌視為替代音軌清單中的項目之一。 因此，<span class="codeph"> MediaPlayerItem.hasAlternateAudio </span>傳回false的唯一情況是當串流完全沒有音訊時。 如果內容只有一個音軌，此方法會傳回true，而<span class="codeph"> MediaPlayerItem.getAudioTracks </span>會傳回包含單一元素（預設音軌）的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> 提供可用替代音軌的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack();  </span> </td> 
   <td colname="3"> 擷取使用<span class="codeph"> selectAudioTrack </span>選取的音軌。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack（AudioTrack音訊Track）  </span> </td> 
   <td colname="3"> 選擇音軌作為當前音軌。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>計時中繼資料</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> 如果串流已關聯計時中繼資料，則返回true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> 提供與流相關聯的定時元資料對象的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>多個描述檔（位元速率）</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> 如果流是多位速率(MBR)流，則為true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;profile&gt; ListgetProfiles();  </span> </td> 
   <td colname="3"> 提供關聯位速率配置檔案的清單。 對於每個配置檔案，可以檢索其位速率以及配置檔案的高度和寬度。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 設定檔getSelectedProfile()  </span> </td> 
   <td colname="3"> 擷取目前選取的描述檔。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>特技遊戲</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported();  </span> </td> 
   <td colname="3"> 如果播放器支援快速前進、倒轉和繼續，則為true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt; Float=""&gt; ListgetAvailablePlaybackRates()  </span> </td> 
   <td colname="3"> 提供特技播放功能內容中可用播放速率的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 浮動getSelectedPlaybackRate()  </span> </td> 
   <td colname="3"> 擷取目前選取的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig()  </span> </td> 
   <td colname="3"> 傳回與此項目關聯的<span class="codeph"> MediaPlayerItemConfig </span>實例。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>媒體資源</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> 傳回與此項目關聯的媒體資源。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId()  </span> </td> 
   <td colname="3"> 傳回與此項目相關的媒體識別碼。 當使用<span class="codeph"> MediaPlayerItemLoader.load </span>載入項目時，就會設定此ID。 </td> 
  </tr> 
 </tbody> 
</table>
