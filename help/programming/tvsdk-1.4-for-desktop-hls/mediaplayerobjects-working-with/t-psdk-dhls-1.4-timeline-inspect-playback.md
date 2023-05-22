---
description: 您可以獲取與TVSDK正在播放的當前選定項關聯的時間線的說明。 當您的應用程式顯示自定義的擦除欄控制項時，此控制項最有用。在該控制項中，可以標識與廣告內容對應的內容節。
title: Inspect播放時間表
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect播放時間表{#inspect-the-playback-timeline}

您可以獲取與TVSDK正在播放的當前選定項關聯的時間線的說明。 當您的應用程式顯示自定義的擦除欄控制項時，此控制項最有用。在該控制項中，可以標識與廣告內容對應的內容節。

下面是如下螢幕抓圖所示的示例實現。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. 訪問 `Timeline` 對象 `MediaPlayer` 使用 `get` 的雙曲餘切值。

   的 `Timeline` 類封裝與時間線內容相關的資訊，該時間線內容與當前由 `MediaPlayer` 實例。 的 `Timeline` 類提供了對基礎時間軸的只讀視圖的訪問。 的 `Timeline` 類提供了獲取所有已放置的getter方法 `TimelineMarker` 對象。

1. 循環訪問清單 `TimelineMarkers` 並使用返回的資訊來實現時間表。

       「TimelineMarker」對象包含兩條資訊：
   
   * 標籤在時間線上的位置（毫秒）
   * 時間線上標籤的持續時間（毫秒）

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
