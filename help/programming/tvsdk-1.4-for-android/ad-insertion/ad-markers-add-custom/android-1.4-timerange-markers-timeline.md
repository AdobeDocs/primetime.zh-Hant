---
description: 此示例顯示了在回放時間線上包含TimeRange規範的建議方法。
title: 將時間範圍和標籤置於時間軸上
exl-id: 53b48d5b-7725-48ae-848a-ccd2a54b132a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 將時間範圍和標籤置於時間軸上 {#place-timerange-ad-markers-on-the-timeline}

此示例顯示了在回放時間線上包含TimeRange規範的建議方法。

1. 將帶外廣告定位資訊轉換為 `TimeRange` 規格(即 `TimeRange` 類)。
1. 使用 `TimeRange` 用於填充實例的規範 `TimeRangeCollection` 類。
1. 傳遞元資料實例，該實例可從 `TimeRangeCollection` 實例，至 `replaceCurrentItem` 方法（MediaPlayer介面的一部分）。
1. 等待TVSDK轉換到 `PREPARED` 等待 `PlaybackEventListener#onPrepared` 要觸發的回調。
1. 通過呼叫 `play()` 方法(部分 `MediaPlayer` 介面)。

* 處理時間線衝突：有些情況下 `TimeRange` 重放時間軸上的規範重疊。 例如，與 `TimeRange` 說明可能低於已放置的結束位置的值。 在這種情況下，TVSDK會靜默地調整違規的開始位置 `TimeRange` 規範以避免時間線衝突。 通過這種調整， `TimeRange` 變得比最初指定的短。 如果調整如此極端，以至於 `TimeRange` TVSDK以靜默方式刪除違規 `TimeRange` 規範。
* 當 `TimeRange` 提供了自定義廣告分段的規範，TVSDK嘗試將它們轉換為分組在廣告分段內的廣告。 TVSDK查找相鄰 `TimeRange` 將它們分成不同的廣告分段。 如果存在與任何其他時間範圍不相鄰的時間範圍，則將其轉換為包含單個廣告的廣告分段。
* 假定正在載入的媒體播放器項目指向VOD資產。 當應用程式嘗試載入元資料包含的媒體資源時，TVSDK會檢查此項 `TimeRange` 只能在自定義ad-marker特徵的上下文中使用的規範。 如果基礎資產不是VOD類型，則TVSDK庫會引發異常。
* 在處理自定義廣告標籤時，TVSDK停用其他廣告解析機制(通過Adobe Primetime廣告決定（以前稱為Auditude）或其它廣告提供系統)。 您可以使用TVSDK提供的各種ad-resolver模組或自定義ad-marker機制中的任一模組。 使用自定義廣告標籤API時，廣告內容被視為已解析並放置在時間軸上。

以下代碼段提供了一個簡單示例，其中將一組三個TimeRange規範作為自定義標籤放在時間軸上。

```java>
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
TimeRangeCollection timeRanges = new TimeRangeCollection();  
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
 
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                               timeRanges.toMetadata(null)); 
 
// prepare the content for playback by creating 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentItem(mediaResource); 
// wait for TVSDK to reach the PREPARED state 
... 
MediaPlayer.PlaybackEventListener playbackEventListener = new 
  MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // TVSDK in in the PREPARED state. We are allowed to start the playback  
        mediaPlayer.play(); 
    } 
} 
```
