---
description: 您可以設定視覺效果，以通知使用者內容正在緩衝。
seo-description: 您可以設定視覺效果，以通知使用者內容正在緩衝。
seo-title: 緩衝
title: 緩衝
uuid: da9498ee-c736-4093-97a2-250d3ad56d49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 2%

---


# 緩衝{#buffering}

您可以設定視覺效果，以通知使用者內容正在緩衝。

監聽`AdobePSDK.PSDKEventType.BUFFERING_BEGIN`和`AdobePSDK.PSDKEventType.BUFFERING_END`事件。 例如：

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

UI Framework提供預設的緩衝覆蓋行為實作，其可延伸，如下所示：

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 
```

DOM的結果如下：

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```

