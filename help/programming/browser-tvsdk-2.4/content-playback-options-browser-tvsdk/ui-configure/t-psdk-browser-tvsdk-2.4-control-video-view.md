---
description: 可以使用MediaPlayerView對象控制視頻視圖的位置和大小。
title: 控制視頻視圖的位置和大小
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 控制視頻視圖的位置和大小{#control-the-position-and-size-of-the-video-view}

可以使用MediaPlayerView對象控制視頻視圖的位置和大小。

預設情況下，瀏覽器TVSDK會嘗試在由於應用程式、配置檔案開關、內容開關等更改而改變視頻大小或位置時保持視頻視圖的縱橫比。

可通過指定不同的長寬比行為來覆蓋預設長寬比行為 *規模策略*。 使用 `MediaPlayerView` 對象 `scalePolicy` 屬性。 的預設縮放策略 `MediaPlayerView` 是使用 `MaintainAspectRatioScalePolicy` 類。 要重置縮放策略，請替換 `MaintainAspectRatioScalePolicy` 上 `MediaPlayerView.scalePolicy` 你自己的政策。

>[!IMPORTANT]
>
>無法設定 `scalePolicy` 屬性。

## 非Flash回退方案 {#non-flash-fallback-scenarios}

在非Flash回退方案中，為使縮放策略正確工作，在中提供的video div元素 `View` 建構子應返回非零值 `offsetWidth` 和 `offsetHeight`。 要提供錯誤函式的示例，有時在css中未顯式設定視頻div元素的寬度和高度時， `View` 建構子返回零 `offsetWidth` 或 `offsetHeight`。

>[!NOTE]
>
>CustomScalePolicy對少數瀏覽器（尤其是IE、Edge和Safari 9）的支援有限。 對於這些瀏覽器，無法更改視頻的本機寬高比。 但是，視頻的位置和尺寸將根據比例策略強制執行。

1. 實施 `MediaPlayerViewScalePolicy` 介面，建立您自己的縮放策略。

   的 `MediaPlayerViewScalePolicy` 有一種方法：

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   例如：

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. 將實施分配給 `MediaPlayerView` 屬性。

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 將視圖添加到媒體播放器 `view` 屬性。

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**例如：縮放視頻以填充整個視頻視圖，而不保持縱橫比：**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```
