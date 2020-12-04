---
description: AdBannerAsset的內容會描述配套的橫幅。
seo-description: AdBannerAsset的內容會描述配套的橫幅。
seo-title: 配套橫幅資料
title: 配套橫幅資料
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 配套橫幅資料{#companion-banner-data}

AdBannerAsset的內容會描述配套的橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`AdobePSDK.PSDKEventType.AD_STARTED`事件返回包含`companionAssets`屬性(`Array<AdBannerAsset>`)的`Ad`實例。
每個`AdBannerAsset`都提供有關顯示資產的資訊。

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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">靜態：資料是靜態影像URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      橫幅資料
    </pre> </td> 
   <td colname="col2"> <span class="codeph"> resourceType</span>為此配套橫幅所指定類型的資料。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時候，配套橫幅可能也會有靜態URL，即影像的直接URL。 </p> <p>如果您不想使用html或iframe，可以使用影像的直接URL。 在這種情況下，您可以使用staticURL來顯示橫幅。 </p> <p>重要： 您必須檢查靜態URL是否為有效字串，因為此屬性可能不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

