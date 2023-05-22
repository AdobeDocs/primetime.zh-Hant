---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: 訪問MediaResource資訊的MediaPlayer屬性
exl-id: 183a2992-06f2-4b1d-84c3-a6c2a7223e32
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 訪問MediaResource資訊的MediaPlayer屬性{#mediaplayer-attributes-to-access-mediaresource-information}

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
   <td colname="1"> 即時流 </td> 
   <td colname="2"> <span class="codeph"> 活 </span> </td> 
   <td colname="3"> 如果流是活的，則為true;如果為VOD，則為false。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 隱藏字幕 </td> 
   <td colname="2"> <span class="codeph"> 有ClosedCaptions </span> </td> 
   <td colname="3"> 如果隱藏字幕磁軌可用，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> 提供可用的隱藏字幕軌道清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptontsTrack </span> </td> 
   <td colname="3"> 檢索與 <span class="codeph"> selectClosedCaptionsTrack </span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> 備用音頻 </td> 
   <td colname="2"> <span class="codeph"> 有備用音頻 </span> </td> 
   <td colname="3"> <p>如果流具有備用音頻軌道，則為True。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 音頻軌道 </span> </td> 
   <td colname="3"> 提供可用備用音頻軌道的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> 選定的音頻軌道 </span> </td> 
   <td colname="3"> 
    <pre>
      檢索當前選定的與 
     <span class="codeph"> 選擇音頻軌道 </span>。 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 定時元資料 </td> 
   <td colname="2"> <span class="codeph"> 有TimedMetadata </span> </td> 
   <td colname="3"> 如果流已關聯定時元資料，則為True。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> 提供與流關聯的定時元資料對象的清單。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> 多個配置檔案（位速率） </td> 
   <td colname="2" morerows="1"> <span class="codeph"> 配置檔案 </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> 提供與此流關聯的關聯比特率配置檔案的清單。 <p>注：可檢索每個輪廓的比特率以及輪廓的高度和寬度。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 媒體資源 </td> 
   <td colname="2"> <span class="codeph"> 資源 </span> </td> 
   <td colname="3"> 返回與此項關聯的媒體資源。 </td> 
  </tr> 
 </tbody> 
</table>
