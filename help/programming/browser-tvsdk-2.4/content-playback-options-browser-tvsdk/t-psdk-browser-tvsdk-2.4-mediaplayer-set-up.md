---
description: MediaPlayer物件會封裝媒體播放器的行為和功能。
title: 設定MediaPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 設定MediaPlay{#set-up-the-mediaplayer}

MediaPlayer物件會封裝媒體播放器的行為和功能。

1. 例項化 `MediaPlayer` 使用下列專案：

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 建立 `MediaPlayerView` 例項：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   位置 `container` 是目標 `div` 包含您的 `HTMLMediaElement`.

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

   呼叫：

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. 附加您的 `MediaPlayerView` 執行個體新增至 `MediaPlayer` 例項：

   ```js
   player.view = view;
   ```

1. 附加自訂控制項 `div` 元素新增至您的MediaPlayer例項。

   例如，在HTML中：

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   呼叫：

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

此 `MediaPlayer` 執行個體現在可供使用，並已正確設定為在裝置熒幕上顯示視訊內容。
