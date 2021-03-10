---
title: 使用UI架構建立基本播放器
description: 使用UI架構建立基本播放器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# 使用UI Framework{#create-a-basic-player-using-the-ui-framework}建立基本播放器

若要使用UI架構建立基本播放器：

1. 為您的播放器例項建立`<div>`。

   例如：

   ```
   <div id="video1" > 
    </div>
   ```

1. 載入播放器。

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   建立播放器時，指定的`<div>`元素會獲得`ptp-main-video-div-style`的CSS類別。 產生的DOM會顯示如下：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. 新增UI控制項。

   例如，新增當滑鼠暫留在播放器上時顯示的控制列：

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   產生的DOM如下：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

從呼叫`ptp.videoPlayer()`傳回的物件會提供包住TVSDK媒體播放器API的行為，並可程式化控制播放。 當您呼叫媒體播放器例項時，使用者介面會根據媒體播放器引發的事件自行更新：

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
