---
description: MediaPlayer對象封裝媒體播放器的行為和功能。
title: 設定MediaPlayer
exl-id: f492b2bb-3280-4306-ac4b-8b8d0fd68409
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 設定MediaPlayer{#set-up-the-mediaplayer}

MediaPlayer對象封裝媒體播放器的行為和功能。

1. 實例化 `MediaPlayer` 使用以下命令：

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 建立 `MediaPlayerView` 實例：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   何處 `container` 是目標 `div` 包含 `HTMLMediaElement`。

   例如，在HTML頁上：

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

1. 連接 `MediaPlayerView` 實例 `MediaPlayer` 實例：

   ```js
   player.view = view;
   ```

1. 附加自定義控制項 `div` 元素。

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

的 `MediaPlayer` 實例現在可用，並且已正確配置為在設備螢幕上顯示視頻內容。
