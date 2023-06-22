---
description: TVSDK通知系統會產生各種錯誤、警告和資訊性通知，提供診斷中繼資料。
title: 通知代碼
exl-id: 7bf016c6-8651-413b-a478-ac2d24f9453c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 概觀 {#notification-codes-overview}

TVSDK通知系統會產生各種錯誤、警告和資訊性通知，提供診斷中繼資料。

通知物件提供與播放器狀態相關的資訊。 TVSDK提供依時間順序排序的通知物件清單。 每個通知都包含以下中繼資料：

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
   <td colname="2"> <p>通知型別。 </p> <p>視平台而定，此屬性是列舉型別，可能值為INFO、WARN和ERROR。 這是通知的頂層群組。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 程式碼</span> </td> 
   <td colname="2"> <p>下列數值表示會指派給通知： 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">錯誤通知事件，從100000到199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">警告通知事件，從200000到299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">從300000到399999的資訊通知事件 </li> 
     </ul> </p> <p>每個頂層範圍（例如錯誤）會分成子範圍(例如從代表播放錯誤的101000到101999)。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 名稱</span> </td> 
   <td colname="2">字串，包含人類看得懂的通知事件說明，例如 <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 中繼資料</span> </td> 
   <td colname="2"> <p>包含通知其他相關資訊的索引鍵/值組。 </p> <p>例如，名為的金鑰 <span class="codeph"> URL</span> 會提供一個與通知相關的URL值，例如造成錯誤的無效URL。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>對另一個的參照 <span class="codeph"> MediaPlayerNotification</span> 直接影響此通知的物件。 </p> <p>一個範例可能是直接對應時間線插入衝突的廣告插入失敗通知。 並非所有通知都會提供內部通知。 </p> </td> 
  </tr> 
 </tbody> 
</table>
