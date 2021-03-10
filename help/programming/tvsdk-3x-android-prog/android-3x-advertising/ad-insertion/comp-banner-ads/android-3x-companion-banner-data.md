---
description: AdAsset的內容會說明配套橫幅。
title: 配套橫幅資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 配套橫幅資料{#companion-banner-data}

AdAsset的內容會說明配套橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

每個`AdAsset`都提供有關顯示資產的資訊。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>可用資訊  </b></th> 
   <th colname="col2" class="entry"> <b>說明</b> </th> 
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
   <td colname="col2"> <p>有時候，配套橫幅也會有<span class="codeph"> staticURL</span>，此為影像或<span class="codeph"> .swf</span>（flash橫幅）的直接URL。 </p> <p>如果您不想使用html或iframe，則可以使用影像或swf的直接URL，在Flash階段中顯示橫幅。 在這種情況下，您可以使用<span class="codeph"> staticURL</span>來顯示橫幅。 </p> <p>重要： 您必須檢查靜態URL是否為有效字串，因為此屬性可能不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>