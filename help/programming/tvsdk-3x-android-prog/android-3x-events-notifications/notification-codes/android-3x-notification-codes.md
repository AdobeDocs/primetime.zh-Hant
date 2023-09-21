---
description: TVSDK通知系統會產生各種錯誤、警告和資訊通知，提供診斷中繼資料。
title: 通知代碼
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 通知代碼 {#notification-codes}

TVSDK通知系統會產生各種錯誤、警告和資訊通知，提供診斷中繼資料。

通知物件會提供與播放器狀態相關的資訊。 TVSDK提供依時間順序排序的通知物件清單。 每個通知都包含下列中繼資料：

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 元素</b></th> 
   <th colname="2" class="entry"><b> 說明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>通知型別。 </p> <p>視平台而定，此屬性是列舉型別，可能值為INFO、WARN和ERROR。 這是通知的最上層分組。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 程式碼</span> </td> 
   <td colname="2"> <p>下列數值表示會指定給通知： 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">從100000到199999的錯誤通知事件 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">警告通知事件，從200000到299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">從300000到399999的資訊通知事件 </li> 
     </ul> </p> <p>每個頂層範圍（例如錯誤）會分成多個子範圍(例如101000到101999表示播放錯誤)。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 名稱</span> </td> 
   <td colname="2">字串，包含人類看得懂的通知事件說明，例如 <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 中繼資料</span> </td> 
   <td colname="2"> <p>包含通知其他相關資訊的金鑰/值組。 </p> <p>例如，名為的索引鍵 <span class="codeph"> URL</span> 會提供一個與通知相關的URL值，例如造成錯誤的無效URL。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>對另一個的參照 <span class="codeph"> MediaPlayerNotification</span> 直接影響此通知的物件。 </p> <p>例如，可能會是直接對應至時間線插入衝突的廣告插入失敗通知。 並非所有通知都會提供內部通知。 </p> </td> 
  </tr> 
 </tbody> 
</table>
