---
description: MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。
title: 用於存取MediaResource資訊的MediaPlayer方法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 用於存取MediaResource資訊的MediaPlayer方法{#mediaplayer-methods-for-accessing-mediaresource-information}

MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> 方法 </th> 
   <th colname="3" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>即時資料流 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isLive()：Boolean； </span> </td> 
   <td colname="3"> <p>如果資料流為即時，則為True；如果為VOD，則為false。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>受DRM保護</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isProtected()：Boolean； </span> </td> 
   <td colname="3"> <p>如果資料流受DRM保護，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式取得drmMetadataInfos()： Vector。&lt;drmmetadatainfo&gt;； </span> </td> 
   <td colname="3"> <p>列出資訊清單中發現的所有DRM中繼資料物件。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>隱藏式字幕</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasClosedCaptions()：Boolean； </span> </td> 
   <td colname="3"> <p>如果可以使用隱藏式字幕追蹤，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get closedCaptionsTracks()：Vector。&lt;closedcaptionstrack&gt;； </span> </td> 
   <td colname="3"> <p>提供可用隱藏式字幕追蹤的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get selectedClosedCaptionsTrack()：ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>擷取目前隱藏式字幕追蹤，選取方式為 <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack： com.adobe.mediacore.info：ClosedCaptionsTrack ) </span> </td> 
   <td colname="3"> <p>將隱藏式字幕軌跡設為目前的隱藏式字幕軌跡。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>替代音軌 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasAlternateAudio()：Boolean； </span> </td> 
   <td colname="3"> <p>如果資料流有替代音訊曲目，則為True。 </p> <p>提示：主要（預設）音軌也是替代音軌清單的一部分。 </p> <p>TVSDK for Desktop HLS將主要音軌視為替代音軌清單中的專案之一。 因此，只有在 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 傳回false表示串流完全沒有音訊。 如果內容只有一個音軌，則此方法會傳回true，並且 <span class="codeph"> 取得音軌 </span> 傳回含有單一元素的清單（預設音軌）。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get audioTracks()：Vector。&lt;audiotrack&gt;； </span> </td> 
   <td colname="3"> 提供可用替代音訊曲目的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get audioTracks()：Vector。&lt;audiotrack&gt;； </span> </td> 
   <td colname="3"> <p>提供可用替代音訊曲目的清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式取得selectedAudioTrack()：AudioTrack； </span> </td> 
   <td colname="3"> <p>擷取選取的音軌 <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack： AudioTrack ) </span> </td> 
   <td colname="3"> <p>選取音訊曲目，做為目前的音訊曲目。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>定時中繼資料</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get hasTimedMetadata()：Boolean； </span> </td> 
   <td colname="3"> <p>如果資料流有關聯的定時中繼資料，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get timedMetadata()：Vector。&lt;timedmetadata&gt;； </span> </td> 
   <td colname="3"> <p>提供與資料流關聯的計時中繼資料物件清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isDynamic()：Boolean； </span> </td> 
   <td colname="3"> <p>如果資料流是多位元速率(MBR)資料流，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式取得設定檔()：Vector。&lt;profile&gt;； </span> </td> 
   <td colname="3"> <p>提供相關位元速率設定檔的清單。 對於每個設定檔，您可以擷取其位元速率以及設定檔的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>特技播放 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get isTrickPlaySupported()：Boolean； </span> </td> 
   <td colname="3"> <p>如果播放器支援快進、倒帶和恢復，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get availablePlaybackRates()：Vector。&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>提供特技播放功能內容中的可用播放速率清單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體播放器 </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get player()：MediaPlayer </span> </td> 
   <td colname="3"> <p>傳回目前與此播放器關聯的媒體播放器。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>媒體資源</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 函式get resource()：MediaResource； </span> </td> 
   <td colname="3"> <p>傳回與此專案關聯的媒體資源。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> 函式get resourceId()：int </span> </td> 
   <td colname="3"> <p>傳回與此專案關聯的媒體識別碼。 </p> </td> 
  </tr> 
 </tbody> 
</table>
