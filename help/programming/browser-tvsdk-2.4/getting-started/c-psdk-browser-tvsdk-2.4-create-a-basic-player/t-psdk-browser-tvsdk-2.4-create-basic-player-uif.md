---
title: 使用UI Framework建立基本播放器
description: 使用UI Framework建立基本播放器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# 使用UI Framework建立基本播放器{#create-a-basic-player-using-the-ui-framework}

若要使用UI Framework建立基本播放器：

1. 建立 `<div>` 用於您的播放器執行個體。

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

   建立播放器時，指定了 `<div>` 元素的CSS類別指定為 `ptp-main-video-div-style`. 產生的DOM如下所示：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. 新增UI控制項。

   例如，新增當滑鼠停留在播放器上時顯示的控制列：

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

   產生的DOM如下所示：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

呼叫傳回的物件 `ptp.videoPlayer()` 提供會包裝TVSDK媒體播放器API的行為，並可以程式設計方式控制播放。 當您在媒體播放器例項上呼叫時，使用者介面會根據媒體播放器引發的事件自我更新：

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
