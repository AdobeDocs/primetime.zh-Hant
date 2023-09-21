---
description: AdAsset的內容會說明隨附橫幅。
title: 隨附橫幅資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 隨附橫幅資料 {#companion-banner-data}

AdAsset的內容會說明隨附橫幅。

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
   <td colname="col2"> 隨附橫幅的寬度（畫素）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 隨附橫幅的高度（畫素）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資源型別 </td> 
   <td colname="col2">此隨附橫幅的資源型別： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html：資料採用HTML程式碼。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe：資料是iframe URL (src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時候，隨附橫幅也會有 <span class="codeph"> staticURL</span> 這是影像或的直接URL。 <span class="codeph"> .swf</span> （flash橫幅）。 </p> <p>如果您不想要使用html或iframe，可以使用影像或swf的直接URL來顯示Flash舞台中的橫幅。 在此情況下，您可以使用 <span class="codeph"> staticURL</span> 以顯示橫幅。 </p> <p>重要：您必須檢查靜態URL是否為有效的字串，因為此屬性可能並不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
