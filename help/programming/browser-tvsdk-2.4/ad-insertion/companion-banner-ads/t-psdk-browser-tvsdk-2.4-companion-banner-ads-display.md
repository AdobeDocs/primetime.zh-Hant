---
description: 要顯示橫幅廣告，您需要建立橫幅廣告實例並允許瀏覽器TVSDK偵聽與廣告相關的事件。
title: 顯示橫幅廣告
exl-id: 331c10a4-ae31-4d3b-aaca-9497e2970ecf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 顯示橫幅廣告 {#display-banner-ads}

要顯示橫幅廣告，您需要建立橫幅廣告實例並允許瀏覽器TVSDK偵聽與廣告相關的事件。

瀏覽器TVSDK提供與通過以下方式的線性廣告關聯的夥伴橫幅廣告的清單： `AdobePSDK.PSDKEventType.AD_STARTED` 的子菜單。

清單可通過以下方式指定伴隨橫幅廣告：

* HTML段
* iFrame頁的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個伴侶廣告，瀏覽器TVSDK會指示哪些類型可用於應用程式。

為事件添加偵聽器 `AdobePSDK.PSDKEventType.AD_STARTED` 執行以下操作：
1. 清除標題實例中的現有廣告。
1. 獲取來自的伴侶廣告清單 `Ad.getCompanionAssets`。
1. 如果伴生廣告清單不為空，則在標題實例的清單上迭代。

   每個標題實例( `AdBannerAsset`)包含寬度、高度、資源類型（html、iframe或static）等資訊，以及顯示伴隨橫幅所需的資料。
1. 如果視頻廣告沒有隨其預訂的伴侶廣告，則伴侶資產清單中不包含該視頻廣告的資料。
1. 將橫幅資訊發送到頁面上在適當位置顯示橫幅的功能。

   這通常是 `div`，您的函式使用 `div ID` 來顯示標題。 例如：

   添加事件偵聽器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   實現監聽程式處理程式：

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

   處理顯示的JavaScript示例：

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
