---
description: TVSDK支援輔助橫幅廣告，這些廣告是線性廣告隨附的廣告，通常會線上性廣告結束後保留在頁面上。 您的應用程式負責顯示隨附線性廣告的配套橫幅。
title: 配套橫幅廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# 配套橫幅廣告{#companion-banner-ads}

TVSDK支援輔助橫幅廣告，這些廣告是線性廣告隨附的廣告，通常會線上性廣告結束後保留在頁面上。 您的應用程式負責顯示隨附線性廣告的配套橫幅。

顯示配套廣告時，請遵循下列建議：

* 嘗試呈現視訊廣告的配套橫幅廣告，以符合您播放器的版面。
* 只有當您的位置完全符合其指定的高度和寬度時，才會呈現配套橫幅。

   >[!TIP]
   >
   >請勿調整橫幅大小。

* 廣告開始後，請盡快呈現配套橫幅。
* 請勿將主廣告／視訊容器與配套橫幅覆蓋。
* 在廣告結束後，繼續顯示配套橫幅。

   標準是顯示每個配套橫幅，直到您取代此橫幅為止。

## 配套橫幅資料{#companion-banner-data}

AdBannerAsset的內容會描述配套的橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`AdPlaybackEvent.AD_STARTED`事件返回包含`companionAssets`屬性(`Vector.<AdAsset>`)的`Ad`實例。
每個`AdAsset`都提供有關顯示資產的資訊。

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
   <td colname="col1"> 橫幅資料 </td> 
   <td colname="col2"> <span class="codeph"> resourceType</span>為此配套橫幅所指定類型的資料。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時候，配套橫幅也會有靜態URL，即影像或<span class="filepath"> .swf</span>（flash橫幅）的直接URL。 </p> <p>如果您不想使用html或iframe，則可以使用影像或swf的直接URL，在Flash階段中顯示橫幅。 在這種情況下，您可以使用staticURL來顯示橫幅。 </p> <p>重要： 您必須檢查靜態URL是否為有效字串，因為此屬性可能不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 顯示橫幅廣告{#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK監聽廣告相關事件。

TVSDK會提供與透過`AdPlaybackEvent.AD_STARTED`事件的線性廣告相關的配套橫幅廣告清單。

清單可透過下列方式指定配套橫幅廣告：

* HTML程式碼片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個配套廣告，TVSDK會指出您的應用程式有哪些類型。

為`AdPlaybackEvent.AD_STARTED`事件添加偵聽器，該事件執行下列操作：

1. 清除橫幅例項中的現有廣告。

1. 從`Ad.companionAssets`取得配套廣告清單。

1. 如果配套廣告清單不是空的，請在橫幅例項清單上重複。

   每個橫幅實例(`AdBannerAsset`)都包含寬度、高度、資源類型（html、iframe或靜態），以及顯示配套橫幅所需的資料。

1. 如果視訊廣告沒有隨附的配套廣告，則配套資產清單中不會包含該視訊廣告的資料。

   若要顯示獨立顯示廣告，請將邏輯新增至指令碼，以在適當的橫幅實例中執行一般的DFP（發佈者的DoubleClick）顯示廣告標籤。

1. 使用`ExternalInterface`將橫幅資訊傳送至您頁面上的函式（通常是JavaScript），該函式會在適當的位置顯示橫幅。

   這通常是`div`，而您的函式使用`div ID`來顯示橫幅。 例如：

   添加事件偵聽器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   實作監聽器處理常式：

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
           for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
               } 
           } 
       }  
       //...        
   }
   ```

   處理顯示的JavaScript範例：

   ```js
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
