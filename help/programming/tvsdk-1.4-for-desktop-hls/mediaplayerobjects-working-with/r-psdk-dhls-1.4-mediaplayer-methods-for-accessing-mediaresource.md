---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
seo-description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
seo-title: 存取MediaResource資訊的MediaPlayer方法
title: 存取MediaResource資訊的MediaPlayer方法
uuid: c2d18f8e-4107-42bc-a975-9b881aadd27b
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# 用於訪問MediaResource資訊的MediaPlayer方法{#mediaplayer-methods-for-accessing-mediaresource-information}

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
   <td colname="1"> <b>即時串流  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isLive():Boolean;  </span> </td> 
   <td colname="3"> <p>如果串流是即時的，則為true;false（如果是VOD）。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>受DRM保護</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isProtected():Boolean;  </span> </td> 
   <td colname="3"> <p>如果流受DRM保護，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get drmMetadataInfos():向量。&lt;drmmetadatainfo&gt;;  </span> </td> 
   <td colname="3"> <p>列出在資訊清單中發現的所有DRM中繼資料物件。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隱藏字幕</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasClosedCaptions():Boolean;  </span> </td> 
   <td colname="3"> <p>如果隱藏字幕音軌可用，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get closedCaptionsTracks():Vector。&lt;closedcaptionstrack&gt;;  </span> </td> 
   <td colname="3"> <p>提供可用隱藏字幕音軌的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get selectedClosedCaptionsTrack():ClosedCaptionsTrack  </span> </td> 
   <td colname="3"> <p>擷取使用<span class="codeph"> SelectClosedCaptionsTrack </span>選取的目前隱藏字幕軌道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack(closedCaptionsTrack:com.adobe.mediacore.info:ClosedCaptionsTrack)  </span> </td> 
   <td colname="3"> <p>將隱藏字幕軌道設定為當前隱藏字幕軌道。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>替代音軌  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasAlternateAudio():Boolean;  </span> </td> 
   <td colname="3"> <p>如果串流有替代的音軌，則為true。 </p> <p>提示： 主音軌（預設）也是替代音軌清單的一部分。 </p> <p>Desktop HLS的TVSDK會將主音軌視為替代音軌清單中的項目之一。 因此，<span class="codeph"> MediaPlayerItem.hasAlternateAudio </span>傳回false的唯一情況是當串流完全沒有音訊時。 如果內容只有一個音軌，此方法會傳回true，而<span class="codeph"> get AudioTracks </span>會傳回包含單一元素（預設音軌）的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get audioTracks():Vector。&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> 提供可用替代音軌的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get audioTracks():Vector。&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> <p>提供可用替代音軌的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get selectedAudioTrack():AudioTrack;  </span> </td> 
   <td colname="3"> <p>擷取使用<span class="codeph"> selectAudioTrack </span>選取的音軌。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack:音軌)  </span> </td> 
   <td colname="3"> <p>選擇音軌作為當前音軌。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>計時中繼資料</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasTimedMetadata():Boolean;  </span> </td> 
   <td colname="3"> <p>如果串流已關聯計時中繼資料，則返回true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get timedMetadata():Vector。&lt;timedmetadata&gt;;  </span> </td> 
   <td colname="3"> <p>提供與流相關聯的定時元資料對象的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isDynamic():Boolean;  </span> </td> 
   <td colname="3"> <p>如果流是多位速率(MBR)流，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get profiles():Vector。&lt;profile&gt;;  </span> </td> 
   <td colname="3"> <p>提供關聯位速率配置檔案的清單。 對於每個配置檔案，可以檢索其位速率以及配置檔案的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>特技遊戲  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isTrickPlaySupported():Boolean;  </span> </td> 
   <td colname="3"> <p>如果播放器支援快速前進、倒轉和繼續，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get availablePlaybackRates():Vector。&lt;number&gt; </span> </td> 
   <td colname="3"> <p>提供特技播放功能內容中可用播放速率的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體播放器  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get player():MediaPlayer  </span> </td> 
   <td colname="3"> <p>傳回目前與此播放器相關聯的媒體播放器。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體資源</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get resource():MediaResource;  </span> </td> 
   <td colname="3"> <p>傳回與此項目關聯的媒體資源。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> 函式get resourceId():int  </span> </td> 
   <td colname="3"> <p>傳回與此項目相關的媒體識別碼。 </p> </td> 
  </tr> 
 </tbody> 
</table>

