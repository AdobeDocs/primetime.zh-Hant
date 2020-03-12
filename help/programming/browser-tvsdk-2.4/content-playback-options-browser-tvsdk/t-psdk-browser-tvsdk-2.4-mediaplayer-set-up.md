---
description: MediaPlayer物件可封裝媒體播放器的行為和功能。
seo-description: MediaPlayer物件可封裝媒體播放器的行為和功能。
seo-title: 設定MediaPlayer
title: 設定MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc

---


# 設定MediaPlayer{#set-up-the-mediaplayer}

MediaPlayer物件可封裝媒體播放器的行為和功能。

1. 使用下列 `MediaPlayer` 項目執行個體化：

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 建立例 `MediaPlayerView` 項：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   其中 `container` 是包含您 `div` 的目標元素 `HTMLMediaElement`。

   例如，在HTML頁面上：

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   來電：

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. 將實例 `MediaPlayerView` 附加到實例 `MediaPlayer` 中：

   ```js
   player.view = view;
   ```

1. 將自訂控制項元 `div` 素附加至您的MediaPlayer例項。

   例如，在HTML中：

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   來電：

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

現在 `MediaPlayer` 可使用此例項，並正確設定以在裝置螢幕上顯示視訊內容。
