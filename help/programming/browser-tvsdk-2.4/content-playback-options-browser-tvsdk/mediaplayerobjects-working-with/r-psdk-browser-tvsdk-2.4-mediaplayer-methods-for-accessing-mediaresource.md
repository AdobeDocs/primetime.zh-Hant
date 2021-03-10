---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: 存取MediaResource資訊的MediaPlayer屬性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 存取MediaResource資訊的MediaPlayer屬性{#mediaplayer-attributes-to-access-mediaresource-information}

MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 目的 </th> 
   <th colname="2" class="entry"> 屬性 </th> 
   <th colname="3" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 即時串流 </td> 
   <td colname="2"> <span class="codeph"> live  </span> </td> 
   <td colname="3"> 如果串流是即時的，則為true;false（如果是VOD）。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 隱藏字幕 </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions  </span> </td> 
   <td colname="3"> 如果隱藏字幕音軌可用，則為true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks  </span> </td> 
   <td colname="3"> 提供可用隱藏字幕音軌的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack  </span> </td> 
   <td colname="3"> 擷取使用<span class="codeph"> selectClosedCaptionsTrack </span>選取的隱藏字幕軌道。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 替代音訊 </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio  </span> </td> 
   <td colname="3"> <p>如果串流有替代的音軌，則為true。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks  </span> </td> 
   <td colname="3"> 提供可用替代音軌的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack  </span> </td> 
   <td colname="3"> 
    <pre>
      擷取目前選取的音軌(以 
     <span class="codeph"> selectAudioTrack </span>。 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 計時中繼資料 </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata  </span> </td> 
   <td colname="3"> 如果串流已關聯計時中繼資料，則返回true。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata  </span> </td> 
   <td colname="3"> 提供與流相關聯的定時元資料對象的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 多個描述檔（位元速率） </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 描述檔  </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 提供與此流關聯的相關比特率配置檔案的清單。 <p>注意： 您可以擷取每個描述檔的位元速率，以及描述檔的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 媒體資源 </td> 
   <td colname="2"> <span class="codeph"> 資源  </span> </td> 
   <td colname="3"> 傳回與此項目關聯的媒體資源。 </td> 
  </tr> 
 </tbody> 
</table>

