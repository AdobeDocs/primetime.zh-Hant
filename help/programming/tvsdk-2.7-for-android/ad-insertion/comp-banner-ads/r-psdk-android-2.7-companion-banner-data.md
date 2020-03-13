---
description: AdAsset的內容會說明配套橫幅。
seo-description: AdAsset的內容會說明配套橫幅。
seo-title: 配套橫幅資料
title: 配套橫幅資料
uuid: 4a5d78e1-5abe-45a8-b50f-14f73fdcc879
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 配套橫幅資料 {#companion-banner-data}

AdAsset的內容會說明配套橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

每個 `AdAsset` 都提供有關顯示資產的資訊。

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
   <td colname="col2"> 配套橫幅的寬度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 配套橫幅的高度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資源類型 </td> 
   <td colname="col2">此配套橫幅的資源類型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:資料是以HTML程式碼表示。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:資料是iframe URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時候，配套橫幅也會有 <span class="codeph"> 靜態URL</span> ，即影像或。swf <span class="codeph"></span> （flash橫幅）的直接URL。 </p> <p>如果您不想使用html或iframe，則可使用影像或swf的直接URL，在Flash階段中顯示橫幅。 在這種情況下，您可以使用 <span class="codeph"> staticURL</span> 來顯示橫幅。 </p> <p>重要： 您必須檢查靜態URL是否為有效字串，因為此屬性可能不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

