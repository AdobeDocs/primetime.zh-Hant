---
description: 當瀏覽器TVSDK偵測到播放清單／資訊清單中的訂閱標籤時，播放器會自動嘗試處理標籤，並將其公開為TimedMetadata物件。
title: 計時中繼資料類別
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 計時中繼資料類別{#timed-metadata-class}

當瀏覽器TVSDK偵測到播放清單／資訊清單中的訂閱標籤時，播放器會自動嘗試處理標籤，並將其公開為TimedMetadata物件。

`TimedMetadata`類提供以下元素：

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
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>以下是計時的中繼資料類型： 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG —— 計時中繼資料是從播放清單／資訊清單中的標籤建立。 </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 —— 計時中繼資料是從媒體串流中的ID3標籤建立。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>時間 </p> </td> 
   <td colname="col02"> <p>數字 </p> </td> 
   <td colname="col2"> <p>相對於主要內容開始的本機時間位置（毫秒），在主要內容開始時，此計時中繼資料會出現在串流中。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>字串 </p> </td> 
   <td colname="col2"> <p>計時中繼資料的唯一識別碼。 </p> <p>通常會從提示／標籤ID屬性中擷取（如果存在）。 否則，它是唯一的隨機值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>名稱 </p> </td> 
   <td colname="col02"> <p>數字 </p> </td> 
   <td colname="col2"> <p>計時中繼資料的名稱。 </p> <p>如果類型為TAG，則值代表提示／標籤名稱。 如果類型為ID3，則值為null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>內容 </p> </td> 
   <td colname="col02"> <p>字串 </p> </td> 
   <td colname="col2"> <p>計時中繼資料的原始內容。 </p> <p>如果類型為TAG，則值代表cue/tag的整個屬性清單。 如果類型id ID3，則值為null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>中繼資料 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 中繼資料</span> </p> </td> 
   <td colname="col2"> <p>從播放清單／資訊清單自訂標籤中處理／擷取的資訊。 </p> </td> 
  </tr> 
 </tbody> 
</table>

