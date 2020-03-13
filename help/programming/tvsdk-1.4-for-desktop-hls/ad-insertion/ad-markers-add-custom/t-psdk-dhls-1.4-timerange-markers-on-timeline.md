---
description: 此範例顯示在播放時間軸中加入TimeRange規格的建議方式。
seo-description: 此範例顯示在播放時間軸中加入TimeRange規格的建議方式。
seo-title: 將TimeRange廣告標籤置於時間軸
title: 將TimeRange廣告標籤置於時間軸
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 將TimeRange廣告標籤置於時間軸 {#place-timerange-ad-markers-on-the-timeline}

此範例顯示在播放時間軸中加入TimeRange規格的建議方式。

1. 將帶外廣告定位資訊轉譯為規格 `TimeRange` 清單(即類別的例 `TimeRange` 項)。
1. 使用一組規 `TimeRange` 格來填入類的實 `TimeRangeCollection` 例。
1. 將可從例項取得的中繼資料例 `TimeRangeCollection` 項傳遞至方 `replaceCurrentItem` 法(介面的一部分 `MediaPlayer` )。
1. 等待觸發回呼，等待TVSDK轉 `PlaybackEventListener#onPrepared` 換至PREPARED狀態。
1. 呼叫方法(介面的一 `play()` 部分)以開始視訊 `MediaPlayer` 播放。

* 處理時間軸衝突：播放時間軸上的某些規 `TimeRange` 格可能會重疊。 例如，與規範對應的起始位置 `TimeRange` 的值可能低於已放置的終止位置的值。 在此情況下，TVSDK會無訊息地調整違規規格的開始位置， `TimeRange` 以避免時間軸衝突。 透過此調整，新增的 `TimeRange` 時間會短於原始指定。 如果調整極端，導致持續時間為 `TimeRange` 零毫秒，TVSDK會無訊息地放棄違規規 `TimeRange` 格。

* 當提 `TimeRange` 供自訂廣告插播的規格時，TVSDK會嘗試將這些轉換為廣告插播內分組的廣告。 TVSDK會尋找相鄰的規 `TimeRange` 格，並將它們叢整合個別的廣告插頁。 如果有時間範圍不與任何其他時間範圍相鄰，則會將它們轉換為包含單一廣告的廣告分段。

* 假設載入的媒體播放器項目指向VOD資產。 當您的應用程式嘗試載入其中繼資料包含只能用於自訂廣告標籤功能內容 `TimeRange` 之規格的媒體資源時，TVSDK會檢查此項。 如果基礎資產不是VOD類型，TVSDK程式庫會擲回例外。

* 在處理自訂廣告標籤時，TVSDK會停用其他廣告解析機制(透過Adobe Primetime廣告決策（先前稱為Auditude）或其他廣告布建系統)。 您可以使用TVSDK提供的各種廣告解析器模組或自訂廣告標籤機制。 使用自訂廣告標籤API時，廣告內容會被視為已解析並置於時間軸上。
>
><!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->


下列程式碼片段提供一個簡單範例，其中將一組三 `TimeRange` 個規格放在時間軸上做為自訂廣告標籤。

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
