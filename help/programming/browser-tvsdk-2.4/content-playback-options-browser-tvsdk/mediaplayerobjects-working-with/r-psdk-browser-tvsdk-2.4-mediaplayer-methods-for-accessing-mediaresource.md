---
description: MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。
title: 用於存取MediaResource資訊的MediaPlayer屬性
exl-id: 183a2992-06f2-4b1d-84c3-a6c2a7223e32
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 用於存取MediaResource資訊的MediaPlayer屬性{#mediaplayer-attributes-to-access-mediaresource-information}

MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 用途 </th> 
   <th colname="2" class="entry"> 屬性 </th> 
   <th colname="3" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 即時資料流 </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> 如果資料流為即時，則為True；如果為VOD，則為False。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 隱藏式字幕 </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> 如果隱藏式字幕追蹤可供使用，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> 提供可用隱藏式字幕追蹤的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> 擷取隱藏式字幕追蹤，該追蹤已選取 <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 替代音訊 </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>如果資料流有替代音訊曲目，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> 提供可用替代音訊曲目的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      擷取目前選取的音軌（選擇於） 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 定時中繼資料 </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> 如果串流有關聯的計時中繼資料，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> 提供與資料流關聯的計時中繼資料物件清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 多個設定檔（位元速率） </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 設定檔 </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 提供與此資料流關聯的位元速率設定檔清單。 <p>注意：您可以擷取每個設定檔的位元速率，以及設定檔的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 媒體資源 </td> 
   <td colname="2"> <span class="codeph"> 資源 </span> </td> 
   <td colname="3"> 傳回與此專案關聯的媒體資源。 </td> 
  </tr> 
 </tbody> 
</table>
