---
description: AdBannerAsset的內容會說明隨附橫幅。
title: 隨附橫幅資料
exl-id: 94954233-4357-43be-a61f-6d8010c930ca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 隨附橫幅資料{#companion-banner-data}

AdBannerAsset的內容會說明隨附橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

此 `AdobePSDK.PSDKEventType.AD_STARTED` 事件傳回 `Ad` 包含 `companionAssets` 屬性( `Array<AdBannerAsset>`)。
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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">靜態：資料是靜態影像URL (src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      橫幅資料
    </pre> </td> 
   <td colname="col2"> 指定的型別資料 <span class="codeph"> resourceType</span> 以取得此隨附橫幅。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時隨附橫幅也可能具有靜態URL，它是影像的直接URL。 </p> <p>如果您不想要使用html或iframe，可以使用影像的直接網址。 在此情況下，您可以使用staticURL來顯示橫幅。 </p> <p>重要：您必須檢查靜態URL是否為有效的字串，因為此屬性可能並不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
