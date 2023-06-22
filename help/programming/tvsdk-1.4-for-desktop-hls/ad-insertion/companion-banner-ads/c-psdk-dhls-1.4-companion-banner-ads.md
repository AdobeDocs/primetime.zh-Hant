---
description: TVSDK支援隨附橫幅廣告，這是線性廣告隨附的廣告，通常線上性廣告結束後仍會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的隨附橫幅。
title: 隨附橫幅廣告
exl-id: c10a38ec-acbb-4e84-aff2-c93c9b1cec81
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 隨附橫幅廣告 {#companion-banner-ads}

TVSDK支援隨附橫幅廣告，這是線性廣告隨附的廣告，通常線上性廣告結束後仍會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的隨附橫幅。

顯示隨附廣告時，請遵循下列建議：

* 嘗試儘可能多地呈現視訊廣告的隨附橫幅廣告，以符合您的播放器版面配置。
* 只有在您的位置完全符合其指定高度和寬度時，才會顯示隨附橫幅。

   >[!TIP]
   >
   >請勿調整橫幅大小。

* 在廣告開始後儘快提供隨附橫幅。
* 請勿以隨附橫幅覆蓋主要廣告/視訊容器。
* 在廣告結束後繼續顯示隨附橫幅。

   標準是顯示每個隨附橫幅，直到您有此橫幅的替代橫幅為止。

## 隨附橫幅資料 {#companion-banner-data}

AdBannerAsset的內容會說明隨附橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

此 `AdPlaybackEvent.AD_STARTED` 事件傳回 `Ad` 包含 `companionAssets` 屬性( `Vector.<AdAsset>`)。
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
   <td colname="col1"> 橫幅資料 </td> 
   <td colname="col2"> 指定的型別資料 <span class="codeph"> resourceType</span> 以取得此隨附橫幅。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時候，隨附橫幅也會有一個staticURL，它是影像或的直接網址。 <span class="filepath"> .swf</span> （flash橫幅）。 </p> <p>如果您不想要使用html或iframe，可以使用影像或swf的直接URL來顯示Flash舞台中的橫幅。 在此情況下，您可以使用staticURL來顯示橫幅。 </p> <p>重要：您必須檢查靜態URL是否為有效的字串，因為此屬性可能並不一定都可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 顯示橫幅廣告 {#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK接聽與廣告相關的事件。

TVSDK提供透過與線性廣告相關聯的隨附橫幅廣告清單 `AdPlaybackEvent.AD_STARTED` 事件事件。

資訊清單可透過以下方式指定隨附橫幅廣告：

* HTML片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個隨附廣告，TVSDK會指出您的應用程式可用的型別。

新增監聽器 `AdPlaybackEvent.AD_STARTED` 具有以下動作的事件：

1. 清除橫幅例項中的現有廣告。

1. 從取得隨附廣告清單 `Ad.companionAssets`.

1. 如果隨附廣告清單不是空的，請在清單上反複檢視橫幅例項。

   每個橫幅例項( `AdBannerAsset`)包含寬度、高度、資源型別（html、iframe或靜態）等資訊，以及顯示隨附橫幅所需的資料。

1. 如果視訊廣告沒有隨附廣告，隨附資產清單則不包含該視訊廣告的資料。

   若要顯示獨立顯示廣告，請在指令碼中新增邏輯，以在適當的橫幅例項中執行一般DFP (DoubleClick for Publishers)顯示廣告標籤。

1. 使用將橫幅資訊傳送至頁面上的函式（通常是JavaScript） `ExternalInterface`，會在適當的位置顯示橫幅。

   這通常是 `div`，而您的函式會使用 `div ID` 以顯示橫幅。 例如：

   新增事件接聽程式：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   實作接聽程式處理常式：

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
