---
description: TVSDK通知系統會產生各種錯誤、警告和資訊通知，以提供診斷中繼資料。
seo-description: TVSDK通知系統會產生各種錯誤、警告和資訊通知，以提供診斷中繼資料。
seo-title: 通知代碼
title: 通知代碼
uuid: a7b77a5c-9873-45cf-8499-aa00270a7ad6
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# 概觀 {#notification-codes-overview}

TVSDK通知系統會產生各種錯誤、警告和資訊通知，以提供診斷中繼資料。

通知物件提供與播放器狀態相關的資訊。 TVSDK提供按時間順序排序的通知物件清單，而每個通知都包含下列中繼資料：

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 元素 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> type </td> 
   <td colname="2"> 通知類型。 根據平台，此屬性會參照可能具有INFO、WARN或ERROR值的列舉類型。 這是通知的頂層群組。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 代碼 </td> 
   <td colname="2">分配給通知的數字表示： 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">錯誤通知事件，從100000到1999999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">警告通知事件，從200000到2999999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">資訊通知事件，從300000到3999999 </li> 
    </ul> <p>每個頂層範圍（例如錯誤）會分成子範圍，例如101000到101999代表播放錯誤。 </p>
    <pre>
     枚舉 <span class="codeph"></span> mediacore.PSDKErrorCode列出可能的值。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 名稱 </td> 
   <td colname="2">包含代碼的人類可讀描述的字串，如 <span class="codeph"> SEEK_ERROR</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 中繼資料 </td> 
   <td colname="2">包含通知其他相關資訊的金鑰／值配對。 例如，名為 <span class="codeph"></span> URL的索引鍵會與與與通知相關的URL值配對，例如導致錯誤的無效URL。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">直接影響此通知 <span class="codeph"> 的其他MediaPlayerNotification</span> 物件的參考。 例如，廣告插入失敗的通知會直接與時間線插入衝突對應。 並非所有通知都提供內部通知。 </td> 
  </tr> 
 </tbody> 
</table>

