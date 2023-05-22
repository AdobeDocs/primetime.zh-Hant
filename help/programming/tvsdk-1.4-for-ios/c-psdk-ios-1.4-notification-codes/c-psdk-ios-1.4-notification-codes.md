---
description: TVSDK通知系統產生各種錯誤、警告和資訊通知，這些通知提供診斷元資料。
title: 通知代碼
exl-id: 6cbc85d7-c197-448b-aa90-554c70af6557
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# TVSDK通知系統 {#tvsdk-notification-system}

TVSDK通知系統產生各種錯誤、警告和資訊通知，這些通知提供診斷元資料。

通知對象提供與播放器狀態相關的資訊。 TVSDK提供按時間順序排序的通知對象清單，每個通知都包含以下元資料：

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 元素 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 類型</span></td> 
   <td colname="2">通知類型。 根據平台，此屬性引用的枚舉類型可能值為 
    <pre>
      資訊、警告或錯誤。 這是通知的頂級分組。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 代碼</span></td> 
   <td colname="2">分配給通知的數字表示法。 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">錯誤通知事件，從100000到199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">警告通知事件，20000至299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">資訊通知事件，從300000到399999 </li> 
    </ul> <p>每個頂級範圍（如錯誤）被劃分為子範圍，如表示回放錯誤的101000到101999。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 名稱</span></td> 
   <td colname="2">包含代碼的人可讀描述的字串，如 <span class="codeph"> 查找錯誤</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 元資料</span> </td> 
   <td colname="2">包含有關通知的其他相關資訊的鍵/值對。 例如，名為 <span class="codeph"> URL</span> 將與與通知相關的URL值配對，如導致錯誤的無效URL。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 內部通知</span></td> 
   <td colname="2">對另一個的引用 <span class="codeph"> PTN認證</span> 直接影響此通知的對象。 示例可能是與時間線插入衝突直接對應的廣告插入失敗的通知。 並非所有通知都提供內部通知。 </td> 
  </tr> 
 </tbody> 
</table>
