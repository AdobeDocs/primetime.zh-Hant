---
description: 當瀏覽器TVSDK在播放清單/清單中檢測到預訂的標籤時，播放器自動嘗試處理該標籤並將其作為TimedMetadata對象公開。
title: 定時元資料類
exl-id: 893879b5-03ed-4c11-80a6-b57b7d54a95c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 定時元資料類{#timed-metadata-class}

當瀏覽器TVSDK在播放清單/清單中檢測到預訂的標籤時，播放器自動嘗試處理該標籤並將其作為TimedMetadata對象公開。

的 `TimedMetadata` 類提供以下元素：

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性 </th> 
   <th colname="col02" class="entry"> 類型 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>類型 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>以下是定時元資料類型： 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG — 定時元資料是從播放清單/清單中的標籤建立的。 </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 — 從媒體流的ID3標籤建立的定時元資料。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>時間 </p> </td> 
   <td colname="col02"> <p>數字 </p> </td> 
   <td colname="col2"> <p>相對於主內容開始的本地時間位置（毫秒），其中流中存在此定時元資料。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID </p> </td> 
   <td colname="col02"> <p>字串 </p> </td> 
   <td colname="col2"> <p>定時元資料的唯一標識符。 </p> <p>通常從提示/標籤ID屬性（如果存在）中提取。 否則，它是唯一的隨機值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>名稱 </p> </td> 
   <td colname="col02"> <p>數字 </p> </td> 
   <td colname="col2"> <p>定時元資料的名稱。 </p> <p>如果類型為TAG，則值表示提示/標籤名稱。 如果類型為ID3，則值為null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>內容 </p> </td> 
   <td colname="col02"> <p>字串 </p> </td> 
   <td colname="col2"> <p>定時元資料的原始內容。 </p> <p>如果類型為TAG，則值表示提示/標籤的整個屬性清單。 如果類型ID3，則值為null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>元資料 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 元資料</span> </p> </td> 
   <td colname="col2"> <p>從播放清單/清單自定義標籤中處理/提取的資訊。 </p> </td> 
  </tr> 
 </tbody> 
</table>
