---
description: 您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。
title: 控制視訊檢視的位置和大小
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 控制視訊檢視的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView物件來控制視訊檢視的位置和大小。

瀏覽器TVSDK預設會在視訊大小或位置因應用程式、設定檔引數、內容引數等變更而改變時，嘗試維持視訊檢視的外觀比例。

您可以透過指定不同的外觀比例行為來覆寫預設外觀比例行為 *縮放原則*. 使用指定縮放原則 `MediaPlayerView` 物件的 `scalePolicy` 屬性。 的預設縮放原則 `MediaPlayerView` 使用的例項設定 `MaintainAspectRatioScalePolicy` 類別。 若要重設比例原則，請取代預設的執行個體 `MaintainAspectRatioScalePolicy` 於 `MediaPlayerView.scalePolicy` 使用您自己的原則。

>[!IMPORTANT]
>
>您無法設定 `scalePolicy` 屬性變更為空值。

## 非Flash遞補案例 {#non-flash-fallback-scenarios}

在非Flash遞補情況中，為了讓縮放原則正確運作，在中提供的視訊div元素 `View` 建構函式應該傳回非零值 `offsetWidth` 和 `offsetHeight`. 若要提供不正確函式的範例，有時當video div元素的寬度和高度未在css中明確設定時，則 `View` 建構函式傳回零 `offsetWidth` 或 `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy對幾個瀏覽器的支援有限，尤其是IE、Edge和Safari 9。 對於這些瀏覽器，無法變更視訊的原生外觀比例。 不過，視訊的位置和維度會根據縮放原則強制執行。

1. 實作 `MediaPlayerViewScalePolicy` 介面以建立您自己的縮放原則。

   此 `MediaPlayerViewScalePolicy` 有一個方法：

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

1. 將檢視新增至媒體播放器的 `view` 屬性。

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**例如：縮放視訊以填滿整個視訊檢視，而不維持外觀比例：**

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
