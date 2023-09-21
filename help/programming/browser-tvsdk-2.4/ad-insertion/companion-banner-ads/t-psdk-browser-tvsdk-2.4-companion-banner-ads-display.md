---
description: 若要顯示橫幅廣告，您必須建立橫幅例項，並允許瀏覽器TVSDK接聽廣告相關事件。
title: 顯示橫幅廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 顯示橫幅廣告 {#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許瀏覽器TVSDK接聽廣告相關事件。

瀏覽器TVSDK提供透過與線性廣告相關的隨附橫幅廣告清單 `AdobePSDK.PSDKEventType.AD_STARTED` 事件。

資訊清單可透過以下方式指定隨附橫幅廣告：

* HTML片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個隨附廣告，瀏覽器TVSDK會指出您的應用程式可用的型別。

新增事件的監聽器 `AdobePSDK.PSDKEventType.AD_STARTED` 這樣會執行下列動作：
1. 清除橫幅例項中的現有廣告。
1. 從取得隨附廣告清單 `Ad.getCompanionAssets`.
1. 如果隨附廣告清單不是空的，請反複檢視橫幅例項的清單。

   每個橫幅例項(一個 `AdBannerAsset`)包含寬度、高度、資源型別（html、iframe或靜態）等資訊，以及顯示隨附橫幅所需的資料。
1. 如果視訊廣告沒有隨附廣告預訂，則隨附資產清單不包含該視訊廣告的資料。
1. 將橫幅資訊傳送至頁面上會在適當位置顯示橫幅的函式。

   這通常是 `div`，而您的函式會使用 `div ID` 以顯示橫幅。 例如：

   新增事件接聽程式：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   實作監聽器處理常式：

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
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
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```
