---
description: 請完成下列步驟，以使用瀏覽器TVSDK建立基本播放器。
seo-description: 請完成下列步驟，以使用瀏覽器TVSDK建立基本播放器。
seo-title: 使用TVSDK建立基本播放器
title: 使用TVSDK建立基本播放器
uuid: ec15cf53-197f-4190-a6b2-600a57815390
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 使用TVSDK{#create-a-basic-player-using-tvsdk}建立基本播放器

請完成下列步驟，以使用瀏覽器TVSDK建立基本播放器。

1. 建立新目錄，您可在其中下載瀏覽器TVSDK的壓縮檔案。
1. 從Zendesk下載瀏覽器TVSDK、解壓縮檔案，並將frameworks檔案夾放入新目錄。
1. 為程式碼建立內含`div`的簡單HTML樣式板。
1. 將此樣式板置於您在步驟1中建立的目錄中的HTML檔案中。

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. 在標題區段中新增瀏覽器TVSDK程式庫。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. 對於body標籤，添加`onLoad`部分。

   ```
   <body onload="startVideo()">
   ```

1. 開始實作`startVideo`函式。
1. 新增指令碼標籤並在標籤中建立`startVideo`函式。

   這應該在頁面的標題區段中。

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. 建立`Adobe.MediaPlayer`。

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 建立`MediaPlayerView`。

   >[!TIP]
   >
   >這是您先前建立的`div`使用的位置。

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 新增播放器事件接聽程式。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 實作事件處理常式，並將它放在新增事件接聽程式之前。

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. 建立`MediaResource`，以傳遞M3U8連結（或mpd）。

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. 建立空配置並替換資源。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. 當播放器處於「已初始化」狀態時，請呼叫`prepareToPlay`。

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 播放器處於PREPARED狀態後，請呼叫`play`。

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

