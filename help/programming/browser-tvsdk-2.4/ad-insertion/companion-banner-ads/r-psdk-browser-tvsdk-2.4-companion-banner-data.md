---
description: AdBannerAsset的內容會描述配套的橫幅。
seo-description: AdBannerAsset的內容會描述配套的橫幅。
seo-title: 配套橫幅資料
title: 配套橫幅資料
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 配套橫幅資料{#companion-banner-data}

AdBannerAsset的內容會描述配套的橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

事 `AdobePSDK.PSDKEventType.AD_STARTED` 件傳回包 `Ad` 含屬性( `companionAssets``Array<AdBannerAsset>`)的例項。
每個 `AdBannerAsset` 都提供有關顯示資產的資訊。

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
    <ph>
      橫幅資料
    </ph> </td> 
   <td colname="col2"> 由此配套橫幅的resourceType指定 <span class="codeph"> 的類型</span> 。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時候，配套橫幅可能也會有靜態URL，即影像的直接URL。 </p> <p>如果您不想使用html或iframe，可以使用影像的直接URL。 在這種情況下，您可以使用staticURL來顯示橫幅。 </p> <p>重要： 您必須檢查靜態URL是否為有效字串，因為此屬性可能不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

