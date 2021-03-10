---
description: 您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。
title: Inspect播放時間軸
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect播放時間軸{#inspect-the-playback-timeline}

您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。

以下是如下螢幕擷取畫面中所示的範例實作。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用`get`方法訪問`MediaPlayer`中的`Timeline`對象。

   `Timeline`類封裝了與`MediaPlayer`實例當前載入的媒體項相關聯的時間軸內容相關的資訊。 `Timeline`類提供對基礎時間軸的只讀視圖的訪問。 `Timeline`類提供了獲取所有已放置`TimelineMarker`對象的getter方法。

1. 重複`TimelineMarkers`清單，並使用傳回的資訊來實作時間軸。

       「TimelineMarker」物件包含兩項資訊：
   
   * 標籤在時間軸上的位置（以毫秒為單位）
   * 時間軸上標籤的持續時間（以毫秒為單位）

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```

