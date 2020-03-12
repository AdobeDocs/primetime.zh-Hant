---
description: 您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。
seo-description: 您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。
seo-title: 檢查播放時間軸
title: 檢查播放時間軸
uuid: d0fe7926-9b9a-4203-a1c7-e57ba25b882e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 檢查播放時間軸 {#inspect-the-playback-timeline}

您可以取得與目前由TVSDK播放之選取項目相關之時間軸的說明。 當應用程式顯示自訂拖曳列控制項時，最有用的方式是識別與廣告內容對應的內容區段。

以下是如下螢幕擷取畫面中所示的範例實作。  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用方 `Timeline` 法訪問 `MediaPlayer` 中的對 `getTimeline()` 像。

   類 `Timeline` 封裝了與時間軸內容相關的資訊，該時間軸內容與實例當前載入的媒體項相關 `MediaPlayer` 聯。 該 `Timeline` 類可訪問基礎時間軸的只讀視圖。 類提 `Timeline` 供了getter方法，該方法通過對象清單提供迭代 `TimelineMarker` 器。

1. 逐步瀏覽清單， `TimelineMarkers` 並使用傳回的資訊來實作時間軸。

       「TimelineMarker」物件包含兩項資訊：
   
   * 標籤在時間軸上的位置（以毫秒為單位）
   * 時間軸上標籤的持續時間（以毫秒為單位）

1. 監聽例 `MediaPlayerEvent.TIMELINE_UPDATED` 項上的事 `MediaPlayer` 件，並實作回 `TimelineUpdatedEventListener.onTimelineUpdated()` 呼。

   此物 `Timeline` 件可呼叫您的監聽器，告知您的應用程式播放時間軸中可能發生的 `OnTimelineUpdated` 變更。

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
