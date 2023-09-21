---
description: 此範例說明在播放時間軸上包含TimeRange規格的建議方式。
title: 將TimeRange廣告標籤放置在時間軸上
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 將TimeRange廣告標籤放置在時間軸上 {#place-timerange-ad-markers-on-the-timeline}

此範例說明在播放時間軸上包含TimeRange規格的建議方式。

1. 將頻外廣告定位資訊轉譯為 `TimeRange` 規格(亦即 `TimeRange` 類別)。
1. 使用集合 `TimeRange` 用於填入 `TimeRangeCollection` 類別。
1. 傳遞中繼資料例項，可從取得 `TimeRangeCollection` 例項，至 `replaceCurrentItem` 方法（MediaPlayer介面的一部分）。
1. 等待TVSDK轉換至 `PREPARED` 等候 `PlaybackEventListener#onPrepared` 要觸發的回呼。
1. 透過呼叫 `play()` 方法(的一部分 `MediaPlayer` 介面)。

* 處理時間表衝突：在某些情況下 `TimeRange` 規格與播放時間軸重疊。 例如，對應至起始位置的值 `TimeRange` 規格可能低於已放置的結束位置值。 在此情況下，TVSDK會以無訊息方式調整違規專案的開始位置 `TimeRange` 規格以避免時間表衝突。 透過此調整，新的 `TimeRange` 會比原先指定的時間更短。 如果調整太過極端，以致於會導致 `TimeRange` 持續時間為零毫秒的TVSDK會以無訊息方式捨棄違規 `TimeRange` 規格。
* 時間 `TimeRange` 提供自訂廣告插播的規格，TVSDK會嘗試將這些轉譯為分組在廣告插播中的廣告。 TVSDK會尋找相鄰的 `TimeRange` 規格並將它們叢集為個別的廣告插播。 如果時間範圍與任何其他時間範圍都不相鄰，則會將其轉譯為包含單一廣告的廣告插播。
* 假設正在載入的媒體播放器專案指向VOD資產。 TVSDK會在應用程式嘗試載入中繼資料包含的媒體資源時檢查此專案 `TimeRange` 僅能用於自訂廣告標籤功能內容的規格。 如果基礎資產不是VOD型別，TVSDK程式庫會擲回例外狀況。
* 處理自訂廣告標籤時，TVSDK會停用其他廣告解決機制(透過Adobe Primetime ad decisioning (先前稱為Auditude)或其他廣告布建系統)。 您可以使用TVSDK提供的各種廣告解析程式模組之一，或是自訂廣告標籤機制。 使用自訂廣告標籤API時，會將廣告內容視為已解析並放置在時間軸上。

下列程式碼片段提供簡單範例，說明一組三個TimeRange規格會作為自訂廣告標籤放置在時間軸上。

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
