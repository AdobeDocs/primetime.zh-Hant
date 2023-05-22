---
description: 可以使用MediaPlayerView對象控制視頻視圖的位置和大小。
title: 控制視頻視圖的位置和大小
exl-id: 5e7ae557-7f2b-4697-85eb-e72d1f43a7fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 控制視頻視圖的位置和大小{#control-the-position-and-size-of-the-video-view}

可以使用MediaPlayerView對象控制視頻視圖的位置和大小。

預設情況下，TVSDK會嘗試在視頻大小或位置發生變化時（由於應用程式或配置檔案開關或內容開關等的更改）保持視頻視圖的寬高比。

可通過指定不同的長寬比行為來覆蓋預設長寬比行為 *規模策略*。 使用 `MediaPlayerView` 對象 `scalePolicy` 屬性。 的 `MediaPlayerView`的預設比例策略是使用 `MaintainAspectRatioScalePolicy` 類。 要重置縮放策略，請替換 `MaintainAspectRatioScalePolicy` 上 `MediaPlayerView.scalePolicy` 你自己的政策。 (無法設定 `scalePolicy` 屬性到空值。)

1. 實施 `MediaPlayerViewScalePolicy` 介面，建立您自己的縮放策略。

   的 `MediaPlayerViewScalePolicy` 有一種方法：

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK使用 `StageVideo` 顯示視頻的對象，因為 `StageVideo` 對象不在顯示清單中， `viewPort` 參數包含視頻的絕對坐標。
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

1. 將實施分配給 `MediaPlayerView` 屬性。

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 將視圖添加到媒體播放器 `view` 屬性。

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**例如：縮放視頻以填充整個視頻視圖，而不保持縱橫比：**

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
