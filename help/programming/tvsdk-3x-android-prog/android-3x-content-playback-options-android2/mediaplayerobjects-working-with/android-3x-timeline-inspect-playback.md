---
description: 您可以獲取與TVSDK正在播放的當前選定項關聯的時間線的說明。 當您的應用程式顯示自定義的擦除欄控制項時，此控制項最有用。在該控制項中，可以標識與廣告內容對應的內容節。
title: Inspect播放時間表
exl-id: 95792354-76f6-44fd-9207-73e862b434e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect播放時間表 {#inspect-the-playback-timeline}

您可以獲取與TVSDK正在播放的當前選定項關聯的時間線的說明。 當您的應用程式顯示自定義的擦除欄控制項時，此控制項最有用。在該控制項中，可以標識與廣告內容對應的內容節。

下面是如下螢幕抓圖所示的示例實現。  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. 訪問 `Timeline` 對象 `MediaPlayer` 使用 `getTimeline()` 的雙曲餘切值。

   的 `Timeline` 類封裝與時間線內容相關的資訊，該時間線內容與當前由 `MediaPlayer` 實例。 的 `Timeline` 類提供了對基礎時間軸的只讀視圖的訪問。 的 `Timeline` 類提供getter方法，通過 `TimelineMarker` 對象。

1. 循環訪問清單 `TimelineMarkers` 並使用返回的資訊來實現時間表。

       「TimelineMarker」對象包含兩條資訊：
   
   * 標籤在時間線上的位置（毫秒）
   * 時間線上標籤的持續時間（毫秒）

1. 聽著 `MediaPlayerEvent.TIMELINE_UPDATED` 事件 `MediaPlayer` 實例，並實現 `TimelineUpdatedEventListener.onTimelineUpdated()` 回叫。

   的 `Timeline` 通過調用您的 `OnTimelineUpdated` 監聽程式。

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
