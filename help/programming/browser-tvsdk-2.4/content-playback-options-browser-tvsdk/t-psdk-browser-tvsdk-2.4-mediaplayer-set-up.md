---
description: MediaPlayer物件可封裝媒體播放器的行為和功能。
seo-description: MediaPlayer物件可封裝媒體播放器的行為和功能。
seo-title: 設定MediaPlayer
title: 設定MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# 設定MediaPlayer{#set-up-the-mediaplayer}

MediaPlayer物件可封裝媒體播放器的行為和功能。

1. 使用下列項目實例化`MediaPlayer`:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 建立`MediaPlayerView`實例：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   其中`container`是包含`HTMLMediaElement`的目標`div`元素。

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

1. 將`MediaPlayerView`實例附加到`MediaPlayer`實例：

   ```js
   player.view = view;
   ```

1. 將自訂控制項`div`元素附加至您的MediaPlayer例項。

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

`MediaPlayer`例項現已可用，並已正確設定，可在裝置螢幕上顯示視訊內容。
