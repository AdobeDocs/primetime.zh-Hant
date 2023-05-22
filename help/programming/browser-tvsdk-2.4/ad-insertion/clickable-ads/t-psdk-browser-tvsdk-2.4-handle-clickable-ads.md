---
description: MediaPlayer提供notifyClick()函式，用於在播放可點擊廣告時調度與廣告相關的事件。 這些事件提供了您的應用可用於提供點擊功能的廣告和廣告中斷資訊。
title: 處理可點擊的廣告
exl-id: 25738592-f3fe-4f13-b2bb-26a5f942cd18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 處理可點擊的廣告 {#handle-clickable-ads}

MediaPlayer提供notifyClick()函式，用於在播放可點擊廣告時調度與廣告相關的事件。 這些事件提供了您的應用可用於提供點擊功能的廣告和廣告中斷資訊。

播放可點擊廣告時，MediaPlayer將觸發以下事件：

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

的 `AdClickedEvent` 包含處理「點擊」功能所需的資訊。

1. 在播放器中提供控制項，供用戶按一下可點擊的廣告。

   這可以是用於捕獲用戶按一下的按鈕或任何其他元素。
1. 為用戶的ad click事件添加事件偵聽器。

   例如：

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 為用戶的按一下事件添加處理程式。

   此處理程式需要提示MediaPlayer啟動 `AdClicked` 的子菜單。

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. 為MediaPlayer廣告啟動、按一下廣告和完成廣告通知添加事件偵聽器。

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. 添加事件處理程式。
a.處理廣告啟動事件。
這可以執行任何操作，例如為用戶設定UI。

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b.處理廣告按一下的事件。
在本示例中，我們從事件獲取廣告資訊，並使用該資訊開啟一個新的瀏覽器窗口：

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c.處理廣告完成事件。

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
