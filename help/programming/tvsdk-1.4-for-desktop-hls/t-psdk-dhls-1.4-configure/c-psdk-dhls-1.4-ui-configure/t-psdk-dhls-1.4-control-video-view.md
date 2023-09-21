---
description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
title: 控制視訊檢視的位置和大小
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 控制視訊檢視的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。

TVSDK預設會在視訊大小或位置變更（由於應用程式、設定檔切換器或內容切換器等所做的變更）時，嘗試維持視訊檢視的外觀比例。

您可以透過指定不同的長寬比來覆寫預設的長寬比行為 *縮放原則*. 使用指定縮放原則 `MediaPlayerView` 物件的 `scalePolicy` 屬性。 此 `MediaPlayerView`的預設縮放原則是以 `MaintainAspectRatioScalePolicy` 類別。 若要重設縮放原則，請取代預設實體 `MaintainAspectRatioScalePolicy` 於 `MediaPlayerView.scalePolicy` 使用您自己的原則。 (您無法設定 `scalePolicy` 屬性轉換為null值。)

1. 實作 `MediaPlayerViewScalePolicy` 介面以建立您自己的縮放原則。

   此 `MediaPlayerViewScalePolicy` 有一個方法：

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK使用 `StageVideo` 顯示視訊的物件，原因如下 `StageVideo` 物件不在顯示清單上， `viewPort` 引數包含視訊的絕對座標。
   >
   >
   >例如：
   >
   >```
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
   >

1. 將您的實作指派給 `MediaPlayerView` 屬性。

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 將檢視新增至媒體播放器的 `view` 屬性。

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**例如：縮放視訊以填滿整個視訊檢視，而不維持外觀比例：**

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
