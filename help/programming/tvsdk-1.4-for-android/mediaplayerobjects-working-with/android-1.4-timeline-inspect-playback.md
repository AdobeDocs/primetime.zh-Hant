---
description: 您可以取得與TVSDK目前播放之所選專案相關聯的時間軸說明。 當應用程式顯示自訂的搓擦列控制項時，這會非常實用，在控制項中會識別與廣告內容相對應的內容區段。
title: Inspect播放時間軸
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect播放時間軸{#inspect-the-playback-timeline}

您可以取得與TVSDK目前播放之所選專案相關聯的時間軸說明。 當應用程式顯示自訂的搓擦列控制項時，這會非常實用，在控制項中會識別與廣告內容相對應的內容區段。

以下是實作範例，如下列熒幕擷取畫面所示。  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. 存取 `Timeline` 中的物件 `MediaPlayer` 使用 `getTimeline` 方法。

   此 `Timeline` 類別會封裝與時間軸內容相關的資訊，該時間軸與目前由載入的媒體專案相關聯 `MediaPlayer` 執行個體。 此 `Timeline` 類別可讓您存取基礎時間軸的唯讀檢視。 此 `Timeline` class提供getter方法，透過清單 `TimelineMarker` 物件。

1. 逐一檢視清單 `TimelineMarkers` 並使用傳回的資訊實施您的時間表。

       &#39;TimelineMarker&#39;物件包含兩個資訊：
   
   * 時間軸上的標籤位置（毫秒）
   * 時間軸上的標籤持續時間（毫秒）

1. 實作監聽器回呼介面 `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 並向 `Timeline` 物件。

   此 `Timeline` 物件可以呼叫您的，通知應用程式播放時間軸中可能發生的變更 `OnTimelineUpdated` 監聽器。

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```
