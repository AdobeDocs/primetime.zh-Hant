---
description: MediaPlayer提供notifyClick()函式，可在可點按廣告播放時傳送廣告相關事件。 這些事件會提供廣告和廣告插播資訊，您的應用程式可使用這些資訊提供點進功能。
title: 處理可點按的廣告
exl-id: 25738592-f3fe-4f13-b2bb-26a5f942cd18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 處理可點按的廣告 {#handle-clickable-ads}

MediaPlayer提供notifyClick()函式，可在可點按廣告播放時傳送廣告相關事件。 這些事件會提供廣告和廣告插播資訊，您的應用程式可使用這些資訊提供點進功能。

MediaPlayer會在可點按廣告播放時觸發下列事件：

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

此 `AdClickedEvent` 包含處理點進函式所需的資訊。

1. 在您的播放器中提供控制項，讓使用者可點按可點按廣告。

   這可能是用於擷取使用者點按的按鈕或任何其他元素。
1. 為使用者的廣告點選事件新增事件監聽器。

   例如：

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 新增使用者點選事件的處理常式。

   此處理常式需要提示MediaPlayer觸發 `AdClicked` 事件。

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

1. 為MediaPlayer廣告開始、廣告點按和廣告完成通知新增事件接聽程式。

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. 新增事件處理器。
a.處理廣告開始事件。
這可以做任何事，例如設定使用者的UI。

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

   b.處理廣告點選事件。
在此範例中，我們會從事件取得廣告資訊，然後使用該資訊開啟新的瀏覽器視窗：

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
