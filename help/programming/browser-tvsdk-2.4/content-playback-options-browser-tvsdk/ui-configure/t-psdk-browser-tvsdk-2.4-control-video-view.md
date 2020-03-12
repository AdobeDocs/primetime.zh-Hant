---
description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
seo-description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
seo-title: 控制視訊檢視的位置和大小
title: 控制視訊檢視的位置和大小
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 控制視訊檢視的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。

依預設，當視訊的大小或位置因應用程式、描述檔開關、內容開關等變更而變更時，瀏覽器TVSDK會嘗試維持視訊檢視的外觀比例。

通過指定不同的比例策略，可以覆蓋預設的外 *觀比例行為*。 使用物件的屬性指 `MediaPlayerView` 定縮放原 `scalePolicy` 則。 預設比例策 `MediaPlayerView` 略與類的實例一起設 `MaintainAspectRatioScalePolicy` 置。 若要重設比例原則，請以您自己的原則 `MaintainAspectRatioScalePolicy` 取代 `MediaPlayerView.scalePolicy` 預設的on例項。

>[!IMPORTANT]
>
>不能將屬 `scalePolicy` 性設定為空值。

## 非Flash備援案例 {#non-flash-fallback-scenarios}

在非Flash備援藍本中，若要讓縮放原則正常運作，建構函式中提供的視訊div元素應傳 `View` 回與的非零 `offsetWidth` 值 `offsetHeight`。 若要提供不正確函式的範例，有時在css中未明確設定視訊div元素的寬度和高度時，建構函式會 `View` 為或傳回零 `offsetWidth` 值 `offsetHeight`。

>[!NOTE]
>
>CustomScalePolicy對一些瀏覽器的支援有限，尤其是IE、Edge和Safari 9。 對於這些瀏覽器，視訊的原生外觀比例無法變更。 不過，視訊的位置和尺寸會根據縮放原則強制執行。

1. 實作介 `MediaPlayerViewScalePolicy` 面以建立您自己的縮放原則。

   它有 `MediaPlayerViewScalePolicy` 一種方法：

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

1. 將您的實作指派給 `MediaPlayerView` 屬性。

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 將您的檢視新增至Media Player的屬 `view` 性。

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**例如：縮放視訊以填滿整個視訊檢視，而不需維持外觀比例：**

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

