---
description: TVSDK通知系統會產生各種錯誤、警告和資訊通知，以提供診斷中繼資料。
title: 通知代碼
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# 概述{#notification-codes-overview}

TVSDK通知系統會產生各種錯誤、警告和資訊通知，以提供診斷中繼資料。

通知物件提供與播放器狀態相關的資訊。 TVSDK提供按時間順序排序的通知物件清單。 每個通知都包含下列中繼資料：

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 元素 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>通知類型。 </p> <p>視平台而定，此屬性為列舉類型，可能的值為INFO、WARN和ERROR。 這是通知的頂層群組。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 代碼</span> </td> 
   <td colname="2"> <p>以下數字表示法會指派給通知： 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">錯誤通知事件，從100000到1999999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">警告通知事件，從200000到2999999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">資訊通知事件，從300000到3999999 </li> 
     </ul> </p> <p>每個頂層範圍（例如錯誤）會分成子範圍，例如101000到101999代表播放錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 名稱</span> </td> 
   <td colname="2">包含通知事件（例如<span class="codeph"> SEEK_ERROR</span>）的人類可讀描述的字串。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 中繼資料</span> </td> 
   <td colname="2"> <p>包含通知其他相關資訊的金鑰／值配對。 </p> <p>例如，名為<span class="codeph"> URL</span>的索引鍵會提供與通知相關的URL值，例如導致錯誤的無效URL。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>對直接影響此通知的其他<span class="codeph"> MediaPlayerNotification</span>物件的參考。 </p> <p>例如，廣告插入失敗的通知會直接與時間線插入衝突對應。 並非所有通知都提供內部通知。 </p> </td> 
  </tr> 
 </tbody> 
</table>

