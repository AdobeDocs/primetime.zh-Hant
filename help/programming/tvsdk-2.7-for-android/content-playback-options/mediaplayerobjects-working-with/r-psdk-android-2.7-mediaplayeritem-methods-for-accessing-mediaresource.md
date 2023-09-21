---
description: MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。
title: 用於存取MediaResource資訊的MediaPlayerItem方法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 用於存取MediaResource資訊的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。

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
   <td colname="2"> <span class="codeph"> 清單&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> 提供用於廣告刊登流程的廣告標籤清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>即時資料流</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值isLive()； </span> </td> 
   <td colname="3"> 如果資料流為即時，則為True；如果為VOD，則為false。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>受DRM保護</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值isProtected()； </span> </td> 
   <td colname="3"> 如果資料流受DRM保護，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;drmmetadatainfo&gt; getDRMMetadataInfos()； </span> </td> 
   <td colname="3"> 列出資訊清單中發現的所有DRM中繼資料物件。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>隱藏式字幕</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值hasClosedCaptions()； </span> </td> 
   <td colname="3"> 如果可以使用隱藏式字幕追蹤，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;closedcaptionstrack&gt; getClosedCationsTracks()； </span> </td> 
   <td colname="3"> 提供可用隱藏式字幕追蹤的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack()； </span> </td> 
   <td colname="3"> 擷取目前隱藏式字幕追蹤，選取方式為 <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> 將隱藏式字幕軌跡設為目前的隱藏式字幕軌跡。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>替代音軌</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值hasAlternateAudio()； </span> </td> 
   <td colname="3"> 如果資料流有替代音訊曲目，則為True。 <p>注意：主要（預設）音軌也是替代音軌清單的一部分。 </p> <p>Android適用的TVSDK會將主要音軌視為替代音軌清單中的專案之一。 因此，只有在 <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> 傳回false表示串流完全沒有音訊。 如果內容只有一個音軌，則此方法會傳回true，並且 <span class="codeph"> MediaPlayerItem.getAudioTracks </span> 傳回含有單一元素的清單（預設音軌）。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;audiotrack&gt; getAudioTracks()； </span> </td> 
   <td colname="3"> 提供可用替代音訊曲目的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack()； </span> </td> 
   <td colname="3"> 擷取選取的音軌 <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> 選取音訊曲目，做為目前的音訊曲目。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>定時中繼資料</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值hasTimedMetadata()； </span> </td> 
   <td colname="3"> 如果資料流有關聯的定時中繼資料，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;timedmetadata&gt; getTimedMetadata()； </span> </td> 
   <td colname="3"> 提供與資料流關聯的計時中繼資料物件清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>多個設定檔（位元速率）</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值isDynamic()； </span> </td> 
   <td colname="3"> 如果資料流是多位元速率(MBR)資料流，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 清單&lt;profile&gt; getProfiles()； </span> </td> 
   <td colname="3"> 提供相關位元速率設定檔的清單。 對於每個設定檔，您可以擷取其位元速率以及設定檔的高度和寬度。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 設定檔getSelectedProfile() </span> </td> 
   <td colname="3"> 擷取目前選取的設定檔。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>特技播放</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 布林值isTrickPlaySupported()； </span> </td> 
   <td colname="3"> 如果播放器支援快進、倒帶和恢復，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> 提供特技播放功能內容中的可用播放速率清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 浮點數getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> 擷取目前選取的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> 傳回 <span class="codeph"> MediaPlayerItemConfig </span> 與此專案關聯的執行個體。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>媒體資源</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource()； </span> </td> 
   <td colname="3"> 傳回與此專案關聯的媒體資源。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> 傳回與此專案關聯的媒體識別碼。 使用載入專案時設定此ID <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
