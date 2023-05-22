---
description: TVSDK支援伴生條幅廣告，這些廣告是線性廣告的附帶廣告，線上性廣告結束後，通常會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的伴隨橫幅。
title: 伴生橫幅廣告
exl-id: c10a38ec-acbb-4e84-aff2-c93c9b1cec81
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 伴生橫幅廣告 {#companion-banner-ads}

TVSDK支援伴生條幅廣告，這些廣告是線性廣告的附帶廣告，線上性廣告結束後，通常會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的伴隨橫幅。

顯示伴侶廣告時，請遵循以下建議：

* 嘗試在播放器佈局中顯示視頻廣告的夥伴橫幅廣告的數量。
* 僅當您的位置與其指定的高度和寬度完全匹配時，才顯示伴隨標題。

   >[!TIP]
   >
   >不要調整橫幅的大小。

* 在廣告開始後盡快呈現伴隨橫幅。
* 不要將主廣告/視頻容器與伴隨橫幅覆蓋。
* 廣告結束後繼續顯示伴隨橫幅。

   標準是顯示每個伴隨橫幅，直到您更換了此橫幅。

## 伴隨橫幅資料 {#companion-banner-data}

AdBannerAsset的內容描述了一個伴生標題。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

的 `AdPlaybackEvent.AD_STARTED` 事件返回 `Ad` 包含實例 `companionAssets` 屬性( `Vector.<AdAsset>`)。
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
   <td colname="col1"> 橫標資料 </td> 
   <td colname="col2"> 指定的類型的資料 <span class="codeph"> 資源類型</span> 這個伴隨的橫幅。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 靜態URL </td> 
   <td colname="col2"> <p>有時，伴生標題還包含靜態URL，該URL是指向影像或指向 <span class="filepath"> .swf</span> （閃屏）。 </p> <p>如果不想使用html或iframe，可以使用指向影像或swf的直接URL來在Flash階段顯示標題。 在這種情況下，可以使用staticURL顯示標題。 </p> <p>重要提示：您必須檢查靜態URL是否是有效字串，因為此屬性可能並不總是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 顯示橫幅廣告 {#display-banner-ads}

要顯示橫幅廣告，您需要建立橫幅實例並允許TVSDK偵聽與廣告相關的事件。

TVSDK提供與通過以下連結的線性廣告關聯的夥伴橫幅廣告的清單： `AdPlaybackEvent.AD_STARTED` 事件事件。

清單可通過以下方式指定伴隨橫幅廣告：

* HTML段
* iFrame頁的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個伴侶廣告，TVSDK會指示哪些類型可用於應用程式。

為 `AdPlaybackEvent.AD_STARTED` 執行以下操作的事件：

1. 清除標題實例中的現有廣告。

1. 獲取來自的伴侶廣告清單 `Ad.companionAssets`。

1. 如果伴生廣告清單不為空，則在標題實例的清單上迭代。

   每個標題實例( `AdBannerAsset`)包含寬度、高度、資源類型（html、iframe或static）等資訊，以及顯示伴隨橫幅所需的資料。

1. 如果視頻廣告沒有隨其預訂的伴侶廣告，則伴侶資產清單中不包含該視頻廣告的資料。

   要顯示獨立顯示廣告，請將邏輯添加到指令碼中，以在相應的標題實例中運行正常的DFP（發佈伺服器的按兩下）顯示廣告標籤。

1. 通過使用 `ExternalInterface`，以在適當的位置顯示橫幅。

   這通常是 `div`，您的函式使用 `div ID` 來顯示標題。 例如：

   添加事件偵聽器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   實現監聽程式處理程式：

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

   處理顯示的JavaScript示例：

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
