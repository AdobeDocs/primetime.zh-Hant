---
description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
seo-description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
seo-title: 控制視訊檢視的位置和大小
title: 控制視訊檢視的位置和大小
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 控制視訊檢視的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。

TVSDK依預設會嘗試在視訊大小或位置變更時（因應用程式、描述檔開關或內容切換等而變更）維持視訊檢視的外觀比例。

通過指定不同的比例策略，可以覆蓋預設的外 *觀比例行為*。 使用物件的屬性指 `MediaPlayerView` 定縮放原 `scalePolicy` 則。 預設 `MediaPlayerView`比例原則會與類別的例項一起設 `MaintainAspectRatioScalePolicy` 定。 若要重設比例原則，請以您自己的原則 `MaintainAspectRatioScalePolicy` 取代 `MediaPlayerView.scalePolicy` 預設的on例項。 (不能將屬 `scalePolicy` 性設定為空值。)

1. 實作介 `MediaPlayerViewScalePolicy` 面以建立您自己的縮放原則。

   它有 `MediaPlayerViewScalePolicy` 一種方法：

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK使用物 `StageVideo` 件來顯示視訊，而由於物件不在 `StageVideo` 顯示清單中，因此參數 `viewPort` 會包含視訊的絕對座標。
   >
   >
   >例如：
   >
   >
   ```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```

1. 將您的實作指派給 `MediaPlayerView` 屬性。

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 將您的檢視新增至Media Player的屬 `view` 性。

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**例如：縮放視訊以填滿整個視訊檢視，而不需維持外觀比例：**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```

