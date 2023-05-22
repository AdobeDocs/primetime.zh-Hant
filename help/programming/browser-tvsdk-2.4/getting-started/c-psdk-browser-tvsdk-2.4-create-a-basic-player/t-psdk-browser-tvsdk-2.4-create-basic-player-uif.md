---
title: 使用UI框架建立基本播放器
description: 使用UI框架建立基本播放器
copied-description: true
exl-id: 78629042-fd87-406b-af42-229e34d48162
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# 使用UI框架建立基本播放器{#create-a-basic-player-using-the-ui-framework}

要使用UI框架建立基本播放器：

1. 建立 `<div>` 你的玩家實例。

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

   建立播放器時， `<div>` 元素被賦給CSS類 `ptp-main-video-div-style`。 結果的DOM顯示如下：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. 添加UI控制項。

   例如，添加當滑鼠懸停在播放器上時顯示的控制欄：

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

   生成的DOM如下所示：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

調用返回的對象 `ptp.videoPlayer()` 提供一種包裝TVSDK媒體播放器API並允許對回放進行寫程式控制的行為。 在媒體播放器實例上進行呼叫時，用戶介面會根據媒體播放器觸發的事件來更新自己：

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
