---
description: 完成以下步驟，使用瀏覽器TVSDK建立基本播放器。
title: 使用TVSDK建立基本播放器
exl-id: ea7485e0-5d15-469b-b8b6-f9604d283492
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 使用TVSDK建立基本播放器{#create-a-basic-player-using-tvsdk}

完成以下步驟，使用瀏覽器TVSDK建立基本播放器。

1. 建立一個新目錄，在該目錄中可以下載Browser TVSDK的壓縮檔案。
1. 從Zendesk下載瀏覽器TVSDK，解壓縮檔案，並將框架資料夾放在新目錄中。
1. 為代碼建立一個簡單的HTML模板 `div` 在裡面。
1. 將此模板置於您在步驟1中建立的目錄中的HTML檔案中。

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

1. 在頭部分添加瀏覽器TVSDK庫。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. 對於body標籤，添加 `onLoad` 的子菜單。

   ```
   <body onload="startVideo()">
   ```

1. 開始實施 `startVideo` 的子菜單。
1. 添加指令碼標籤並建立 `startVideo` 的子菜單。

   這本該在頁首部分。

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. 建立 `Adobe.MediaPlayer`。

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 建立 `MediaPlayerView`。

   >[!TIP]
   >
   >這裡 `div` 將使用您以前建立的。

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 添加播放器事件偵聽器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 實現事件處理程式，並將其置於添加事件偵聽器之前。

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

1. 建立 `MediaResource`，它通過M3U8鏈路（或mpd）。

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

1. 當播放器處於INITIALIZED狀態時，調用 `prepareToPlay`。

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 玩家處於PREPARED狀態後，呼叫 `play`。

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
