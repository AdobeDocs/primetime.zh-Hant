---
description: 您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。
seo-description: 您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。
seo-title: 檢查播放時間軸
title: 檢查播放時間軸
uuid: 2f903493-2d88-4af2-ac71-36300b49735b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 檢查播放時間軸{#inspect-the-playback-timeline}

您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。

以下是如下螢幕擷取畫面中所示的範例實作。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用方 `Timeline` 法訪問 `MediaPlayer` 中的對 `get` 像。

   類 `Timeline` 封裝了與時間軸內容相關的資訊，該時間軸內容與實例當前載入的媒體項相關 `MediaPlayer` 聯。 該 `Timeline` 類可訪問基礎時間軸的只讀視圖。 類提 `Timeline` 供了獲取所有已放置對象的getter `TimelineMarker` 方法。

1. 逐步瀏覽清單， `TimelineMarkers` 並使用傳回的資訊來實作時間軸。

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

