---
description: TVSDK通知系統產生各種錯誤、警告和資訊通知，這些通知提供診斷元資料。
title: 通知代碼
exl-id: b0a0f14d-e799-4c4d-a233-bc355ec46d78
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 通知代碼 {#notification-codes}

TVSDK通知系統產生各種錯誤、警告和資訊通知，這些通知提供診斷元資料。

通知對象提供與播放器狀態相關的資訊。 TVSDK提供按時間順序排序的通知對象清單。 每個通知都包含以下元資料：

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 元素</b></th> 
   <th colname="2" class="entry"><b> 說明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 類型</span> </td> 
   <td colname="2"> <p>通知類型。 </p> <p>根據平台，此屬性是可能值為INFO、WARN和ERROR的枚舉類型。 這是通知的頂級分組。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> 代碼</span> </td> 
   <td colname="2"> <p>以下數字表示法被分配給通知： 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">錯誤通知事件，從100000到199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">警告通知事件，20000至299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">資訊通知事件，從300000到399999 </li> 
     </ul> </p> <p>每個頂級範圍（如錯誤）被劃分為子範圍，如表示回放錯誤的101000到101999。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 名稱</span> </td> 
   <td colname="2">包含通知事件的可人讀描述的字串，如 <span class="codeph"> 查找錯誤</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 元資料</span> </td> 
   <td colname="2"> <p>包含有關通知的其他相關資訊的鍵/值對。 </p> <p>例如，名為 <span class="codeph"> URL</span> 將提供與通知相關的URL值，例如導致錯誤的無效URL。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 內部通知</span> </td> 
   <td colname="2"> <p>對另一個的引用 <span class="codeph"> 媒體播放器通知</span> 直接影響此通知的對象。 </p> <p>示例可能是與時間線插入衝突直接對應的廣告插入失敗的通知。 並非所有通知都提供內部通知。 </p> </td> 
  </tr> 
 </tbody> 
</table>
