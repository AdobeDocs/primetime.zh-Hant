---
description: AdAsset的內容描述了一個伴生標題。
title: 伴隨橫幅資料
exl-id: 922577fd-bc58-4669-b051-fe54b197a5f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 伴隨橫幅資料 {#companion-banner-data}

AdAsset的內容描述了一個伴生標題。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

每個 `AdAsset` 提供有關顯示資產的資訊。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 可用資訊 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 寬度 </td> 
   <td colname="col2"> 配對標題的寬度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 陪同橫幅的高度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資源類型 </td> 
   <td colname="col2">此伴隨標題的資源類型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:資料在HTML代碼中。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:資料是iframe URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時，伴隨的橫幅上還有 <span class="codeph"> 靜態URL</span> 是指向影像或 <span class="codeph"> .swf</span> （閃屏）。 </p> <p>如果不想使用html或iframe，可以使用指向影像或swf的直接URL來在Flash階段顯示標題。 在這種情況下，您可以 <span class="codeph"> 靜態URL</span> 來顯示標題。 </p> <p>重要提示：您必須檢查靜態URL是否是有效字串，因為此屬性可能並不總是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
