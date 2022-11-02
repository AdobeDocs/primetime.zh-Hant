---
description: 您可以取得與TVSDK目前播放之選取項目相關聯的時間軸說明。 當您的應用程式顯示自訂拖曳列控制項時，這項功能會非常實用，因為系統會識別與廣告內容對應的內容區段。
title: Inspect播放時間軸
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Inspect播放時間軸{#inspect-the-playback-timeline}

您可以取得與TVSDK目前播放之選取項目相關聯的時間軸說明。 當您的應用程式顯示自訂拖曳列控制項時，這項功能會非常實用，因為系統會識別與廣告內容對應的內容區段。

以下是如下列螢幕擷取畫面所示的實作範例。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. 存取 `Timeline` 物件(在 `MediaPlayer` 使用 `get` 方法。

   此 `Timeline` 類封裝與當前由載入的媒體項關聯的時間線內容相關的資訊 `MediaPlayer` 例項。 此 `Timeline` 類別可讓您存取基礎時間軸的唯讀檢視。 此 `Timeline` 類提供了獲取所有已放置的getter方法 `TimelineMarker` 對象。

1. 查看 `TimelineMarkers` 並使用傳回的資訊來實作時間軸。

       「TimelineMarker」對象包含兩條資訊：
   
   * 標籤在時間軸上的位置（以毫秒為單位）
   * 時間軸上的標籤持續時間（以毫秒為單位）

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
