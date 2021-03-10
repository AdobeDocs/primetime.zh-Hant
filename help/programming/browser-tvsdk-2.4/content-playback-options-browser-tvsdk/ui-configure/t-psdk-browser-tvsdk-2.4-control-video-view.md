---
description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
title: 控制視訊檢視的位置和大小
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# 控制視訊檢視的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。

依預設，當視訊的大小或位置因應用程式、描述檔開關、內容開關等變更而變更時，瀏覽器TVSDK會嘗試維持視訊檢視的外觀比例。

通過指定不同的&#x200B;*比例策略*，可以覆蓋預設長寬比行為。 使用`MediaPlayerView`物件的`scalePolicy`屬性指定縮放原則。 預設縮放原則`MediaPlayerView`是以`MaintainAspectRatioScalePolicy`類別的例項設定。 若要重設比例原則，請以您自己的原則取代`MediaPlayerView.scalePolicy`上的預設例項`MaintainAspectRatioScalePolicy`。

>[!IMPORTANT]
>
>不能將`scalePolicy`屬性設定為空值。

## 非Flash備援藍本{#non-flash-fallback-scenarios}

在非Flash的備援藍本中，為使縮放原則正常運作，`View`建構函式中提供的視訊div元素應傳回`offsetWidth`和`offsetHeight`的非零值。 若要提供不正確的函式範例，有時在css中未明確設定視訊div元素的寬度和高度時，`View`建構函式會針對`offsetWidth`或`offsetHeight`傳回零。

>[!NOTE]
>
>CustomScalePolicy對一些瀏覽器的支援有限，尤其是IE、Edge和Safari 9。 對於這些瀏覽器，視訊的原生外觀比例無法變更。 不過，視訊的位置和尺寸會根據縮放原則強制執行。

1. 實作`MediaPlayerViewScalePolicy`介面以建立您自己的縮放原則。

   `MediaPlayerViewScalePolicy`有一個方法：

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

1. 將實施指派給`MediaPlayerView`屬性。

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 將您的檢視新增至Media Player的`view`屬性。

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

