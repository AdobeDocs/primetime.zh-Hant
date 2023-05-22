---
description: AdBannerAsset的內容描述了一個伴生標題。
title: 伴隨橫幅資料
exl-id: 94954233-4357-43be-a61f-6d8010c930ca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 伴隨橫幅資料{#companion-banner-data}

AdBannerAsset的內容描述了一個伴生標題。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

的 `AdobePSDK.PSDKEventType.AD_STARTED` 事件返回 `Ad` 包含實例 `companionAssets` 屬性( `Array<AdBannerAsset>`)。
每個 `AdBannerAsset` 提供有關顯示資產的資訊。

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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">靜態：資料是靜態影像URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      橫標資料
    </pre> </td> 
   <td colname="col2"> 指定的類型的資料 <span class="codeph"> 資源類型</span> 這個伴隨的橫幅。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時，伴隨橫幅可能還包含靜態URL，該URL是指向影像的直接URL。 </p> <p>如果不想使用html或iframe，可以使用影像的直接URL。 在這種情況下，可以使用staticURL顯示標題。 </p> <p>重要提示：您必須檢查靜態URL是否是有效字串，因為此屬性可能並不總是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
