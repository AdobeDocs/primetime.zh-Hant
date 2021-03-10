---
description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
title: 控制視訊檢視的位置和大小
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# 控制視訊檢視的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。

TVSDK依預設會嘗試在視訊大小或位置變更時（因應用程式、描述檔開關或內容切換等而變更）維持視訊檢視的外觀比例。

通過指定不同的&#x200B;*比例策略*，可以覆蓋預設長寬比行為。 使用`MediaPlayerView`物件的`scalePolicy`屬性指定縮放原則。 `MediaPlayerView`的預設比例策略是使用`MaintainAspectRatioScalePolicy`類的實例設定的。 若要重設比例原則，請以您自己的原則取代`MediaPlayerView.scalePolicy`上的預設例項`MaintainAspectRatioScalePolicy`。 （不能將`scalePolicy`屬性設定為空值。）

1. 實作`MediaPlayerViewScalePolicy`介面以建立您自己的縮放原則。

   `MediaPlayerViewScalePolicy`有一個方法：

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK使用`StageVideo`物件來顯示視訊，而由於`StageVideo`物件不在顯示清單中，因此`viewPort`參數會包含視訊的絕對座標。
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

1. 將實施指派給`MediaPlayerView`屬性。

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 將您的檢視新增至Media Player的`view`屬性。

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

