---
description: 當瀏覽器TVSDK偵測到播放清單/資訊清單中有訂閱的標籤時，播放器會自動嘗試處理該標籤，並將其公開為TimedMetadata物件。
title: 定時中繼資料類別
exl-id: 893879b5-03ed-4c11-80a6-b57b7d54a95c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 定時中繼資料類別{#timed-metadata-class}

當瀏覽器TVSDK偵測到播放清單/資訊清單中有訂閱的標籤時，播放器會自動嘗試處理該標籤，並將其公開為TimedMetadata物件。

此 `TimedMetadata` class提供下列元素：

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性 </th> 
   <th colname="col02" class="entry"> 型別 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>以下是計時中繼資料型別： 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">標籤 — 計時中繼資料是從播放清單/資訊清單中的標籤建立的。 </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 — 定時中繼資料是從媒體資料流中的ID3標籤建立的。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>時間 </p> </td> 
   <td colname="col02"> <p>數字 </p> </td> 
   <td colname="col2"> <p>相對於主要內容開始的本機時間位置（毫秒），此計時中繼資料存在於資料流中。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>字串 </p> </td> 
   <td colname="col2"> <p>計時中繼資料的唯一識別碼。 </p> <p>通常從提示/標籤ID屬性（如果存在）中擷取。 否則，它是一個唯一的隨機值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>名稱 </p> </td> 
   <td colname="col02"> <p>數字 </p> </td> 
   <td colname="col2"> <p>計時中繼資料的名稱。 </p> <p>如果型別為TAG，則值代表提示/標籤名稱。 如果型別是ID3，則值為null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>內容 </p> </td> 
   <td colname="col02"> <p>字串 </p> </td> 
   <td colname="col2"> <p>計時中繼資料的原始內容。 </p> <p>如果型別為TAG，則值表示提示/標籤的整個屬性清單。 如果型別ID ID3，則值為Null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>中繼資料 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 中繼資料</span> </p> </td> 
   <td colname="col2"> <p>從播放清單/資訊清單自訂標籤中處理/擷取的資訊。 </p> </td> 
  </tr> 
 </tbody> 
</table>
