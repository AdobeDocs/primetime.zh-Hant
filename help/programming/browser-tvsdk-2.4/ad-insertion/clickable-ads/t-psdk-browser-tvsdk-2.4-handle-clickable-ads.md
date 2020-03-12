---
description: MediaPlayer提供notifyClick()函式，可在播放可點按廣告時分派廣告相關事件。 這些事件提供廣告和廣告分段資訊，供您的應用程式用來提供點進功能。
seo-description: MediaPlayer提供notifyClick()函式，可在播放可點按廣告時分派廣告相關事件。 這些事件提供廣告和廣告分段資訊，供您的應用程式用來提供點進功能。
seo-title: 處理可點選廣告
title: 處理可點選廣告
uuid: 5d3c9d36-60d7-4272-a523-7d1fe0e1615f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 處理可點選廣告 {#handle-clickable-ads}

MediaPlayer提供notifyClick()函式，可在播放可點按廣告時分派廣告相關事件。 這些事件提供廣告和廣告分段資訊，供您的應用程式用來提供點進功能。

當可點按廣告播放時，MediaPlayer會觸發下列事件：

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

包 `AdClickedEvent` 含處理點進功能所需的資訊。

1. 在您的播放器中提供控制項，讓使用者按一下可點選的廣告。

   這可以是用於擷取使用者點按的按鈕或任何其他元素。
1. 新增使用者廣告點按事件的事件接聽程式。

   例如：

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 新增使用者點按事件的處理常式。

   此處理常式需要提示MediaPlayer以觸發事 `AdClicked` 件。

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

1. 新增MediaPlayer廣告開始、點按廣告和完成廣告通知的事件接聽程式。

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. 新增事件處理常式。
a.處理廣告開始事件。
這可以執行任何動作，例如為使用者設定UI。

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

   b.處理廣告點按事件。
在此範例中，我們會從事件中取得廣告資訊，並使用該資訊開啟新的瀏覽器視窗：

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
