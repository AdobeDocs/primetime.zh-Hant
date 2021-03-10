---
description: 此範例顯示在播放時間軸中加入TimeRange規格的建議方式。
title: 將TimeRange廣告標籤置於時間軸
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# 將TimeRange廣告標籤置於時間軸{#place-timerange-ad-markers-on-the-timeline}

此範例顯示在播放時間軸中加入TimeRange規格的建議方式。

1. 將帶外廣告定位資訊轉換為`TimeRange`規範清單（即`TimeRange`類的實例）。
1. 使用`TimeRange`規範集填充`TimeRangeCollection`類的實例。
1. 將可從`TimeRangeCollection`例項取得的中繼資料例項傳遞至`replaceCurrentItem`方法（MediaPlayer介面的一部分）。
1. 等候TVSDK等候觸發`PlaybackEventListener#onPrepared`回呼，以轉換至`PREPARED`狀態。
1. 呼叫`play()`方法（`MediaPlayer`介面的一部分），開始播放視訊。

* 處理時間軸衝突：有時，播放時間軸上的某些`TimeRange`規範會重疊。 例如，與`TimeRange`規範對應的起始位置的值可能低於已放置的終止位置的值。 在此情況下，TVSDK會無訊息地調整違規`TimeRange`規格的開始位置，以避免時間軸衝突。 通過此調整，新`TimeRange`將比最初指定的短。 如果調整極端，以致於會導致持續時間為零毫秒的`TimeRange`,TVSDK會無訊息地捨棄違規的`TimeRange`規格。
* 當提供自訂廣告插播的`TimeRange`規格時，TVSDK會嘗試將這些規格轉換為廣告插播內分組的廣告。 TVSDK會尋找相鄰的`TimeRange`規格，並將它們叢集為個別的廣告插頁。 如果有時間範圍不與任何其他時間範圍相鄰，則會將它們轉換為包含單一廣告的廣告分段。
* 假設載入的媒體播放器項目指向VOD資產。 當您的應用程式嘗試載入中繼資料包含`TimeRange`規格的媒體資源時，TVSDK會檢查此項，這些規格僅能用於自訂廣告標籤功能的內容。 如果基礎資產不是VOD類型，TVSDK程式庫會擲回例外。
* 處理自訂廣告標籤時，TVSDK會停用其他廣告解析機制(透過Adobe Primetime廣告決策（先前稱為Auditude）或其他廣告布建系統)。 您可以使用TVSDK提供的各種廣告解析器模組或自訂廣告標籤機制。 使用自訂廣告標籤API時，廣告內容會被視為已解析並置於時間軸上。

下列程式碼片段提供一個簡單範例，其中將一組三個TimeRange規格放在時間軸上做為自訂廣告標籤。

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
