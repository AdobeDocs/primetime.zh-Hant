---
description: TVSDK通知系統會產生各種錯誤、警告和資訊性通知，提供診斷中繼資料。
title: 通知代碼
exl-id: 615de4e4-fb42-4159-b572-da7866df4ce3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 通知代碼{#notification-codes}

TVSDK通知系統會產生各種錯誤、警告和資訊性通知，提供診斷中繼資料。

通知物件提供與播放器狀態相關的資訊。 TVSDK提供依時間順序排序的通知物件清單，每個通知都包含以下中繼資料：

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 元素 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2">通知型別。 根據平台，此屬性會參考可能值為 <span class="codeph"> 資訊</span>， <span class="codeph"> 警告</span>，或 <span class="codeph"> 錯誤</span>. 這是通知的頂層群組。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 程式碼</span> </td> 
   <td colname="2">指定給通知的數字表示： 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">錯誤通知事件，從100000到199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">警告通知事件，從200000到299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">從300000到399999的資訊通知事件 </li> 
    </ul> <p>每個頂層範圍（例如錯誤）會分成子範圍(例如從代表播放錯誤的101000到101999)。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 名稱</span> </td> 
   <td colname="2">字串，包含人類看得懂的程式碼說明，例如 <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 中繼資料</span> </td> 
   <td colname="2">包含通知其他相關資訊的索引鍵/值組。 例如，名為的金鑰 <span class="codeph"> URL</span> 將與與通知相關的URL值（例如導致錯誤的無效URL）配對。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">對另一個的參照 <span class="codeph"> MediaPlayerNotification</span> 直接影響此通知的物件。 一個範例可能是直接對應時間線插入衝突的廣告插入失敗通知。 並非所有通知都會提供內部通知。 </td> 
  </tr> 
 </tbody> 
</table>
