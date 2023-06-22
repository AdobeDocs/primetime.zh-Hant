---
description: 您可以取得與TVSDK正在播放的目前選取專案相關聯的時間軸說明。 如果您的應用程式顯示自訂的清除列控制項，且其中已識別與廣告內容對應的內容區段，這會是最實用的功能。
title: Inspect播放時間軸
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect播放時間軸{#inspect-the-playback-timeline}

您可以取得與TVSDK正在播放的目前選取專案相關聯的時間軸說明。 如果您的應用程式顯示自訂的清除列控制項，且其中已識別與廣告內容對應的內容區段，這會是最實用的功能。

以下是實作範例，如下方熒幕擷取畫面所示。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. 存取 `Timeline` 中的物件 `MediaPlayer` 使用 `get` 方法。

   此 `Timeline` 類別會封裝與時間軸內容相關的資訊，該時間軸與目前由載入的媒體專案相關聯 `MediaPlayer` 執行個體。 此 `Timeline` 類別可讓您存取基礎時間軸的唯讀檢視。 此 `Timeline` class提供getter方法，用來取得所有放置的 `TimelineMarker` 物件。

1. 逐一檢視清單 `TimelineMarkers` 並使用傳回的資訊來實施您的時間表。

       &#39;TimelineMarker&#39;物件包含兩則資訊：
   
   * 標籤在時間軸上的位置（以毫秒為單位）
   * 時間軸上的標籤持續時間（毫秒）

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
