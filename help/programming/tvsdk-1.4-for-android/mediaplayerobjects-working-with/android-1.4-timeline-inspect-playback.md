---
description: 您可以取得與TVSDK正在播放的目前選取專案相關聯的時間軸說明。 如果您的應用程式顯示自訂的清除列控制項，且其中已識別與廣告內容對應的內容區段，這會是最實用的功能。
title: Inspect播放時間軸
exl-id: af373f1e-ed5b-40a9-a91e-9eb0e4a181de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect播放時間軸{#inspect-the-playback-timeline}

您可以取得與TVSDK正在播放的目前選取專案相關聯的時間軸說明。 如果您的應用程式顯示自訂的清除列控制項，且其中已識別與廣告內容對應的內容區段，這會是最實用的功能。

以下是實作範例，如下方熒幕擷取畫面所示。  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. 存取 `Timeline` 中的物件 `MediaPlayer` 使用 `getTimeline` 方法。

   此 `Timeline` 類別會封裝與時間軸內容相關的資訊，該時間軸與目前由載入的媒體專案相關聯 `MediaPlayer` 執行個體。 此 `Timeline` 類別可讓您存取基礎時間軸的唯讀檢視。 此 `Timeline` class提供getter方法，可透過 `TimelineMarker` 物件。

1. 逐一檢視清單 `TimelineMarkers` 並使用傳回的資訊來實施您的時間表。

       &#39;TimelineMarker&#39;物件包含兩則資訊：
   
   * 標籤在時間軸上的位置（以毫秒為單位）
   * 時間軸上的標籤持續時間（毫秒）

1. 實作監聽器回呼介面 `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 並向 `Timeline` 物件。

   此 `Timeline` 物件可以呼叫您的，通知您的應用程式播放時間軸中可能會發生的變更 `OnTimelineUpdated` 接聽程式。

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
