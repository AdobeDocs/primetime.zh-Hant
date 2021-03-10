---
description: 若要顯示橫幅廣告，您必須建立橫幅例項，並允許瀏覽器TVSDK監聽廣告相關事件。
title: 顯示橫幅廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 顯示橫幅廣告{#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許瀏覽器TVSDK監聽廣告相關事件。

瀏覽器TVSDK會提供與透過`AdobePSDK.PSDKEventType.AD_STARTED`事件的線性廣告相關的配套橫幅廣告清單。

清單可透過下列方式指定配套橫幅廣告：

* HTML程式碼片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個配套廣告，瀏覽器TVSDK會指出您的應用程式有哪些類型。

為`AdobePSDK.PSDKEventType.AD_STARTED`事件添加偵聽程式，該事件執行以下操作：
1. 清除橫幅例項中的現有廣告。
1. 從`Ad.getCompanionAssets`取得配套廣告清單。
1. 如果配套廣告清單不是空的，請在橫幅例項清單上重複。

   每個橫幅實例(`AdBannerAsset`)都包含寬度、高度、資源類型（html、iframe或靜態），以及顯示配套橫幅所需的資料。
1. 如果視訊廣告沒有隨附的配套廣告，則配套資產清單中不會包含該視訊廣告的資料。
1. 將橫幅資訊傳送至頁面上顯示適當位置橫幅的函式。

   這通常是`div`，而您的函式使用`div ID`來顯示橫幅。 例如：

   添加事件偵聽器：

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

