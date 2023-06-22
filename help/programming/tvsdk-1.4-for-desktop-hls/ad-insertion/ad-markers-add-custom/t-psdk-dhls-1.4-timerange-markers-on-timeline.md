---
description: 此範例說明在播放時間軸上包含TimeRange規格的建議方法。
title: 將TimeRange廣告標籤放置在時間軸上
exl-id: a4d45395-38a4-4345-9ba3-87cd9200b9f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 將TimeRange廣告標籤放置在時間軸上 {#place-timerange-ad-markers-on-the-timeline}

此範例說明在播放時間軸上包含TimeRange規格的建議方法。

1. 將頻外廣告定位資訊轉譯為 `TimeRange` 規格(亦即 `TimeRange` 類別)。
1. 使用集合 `TimeRange` 填入 `TimeRangeCollection` 類別。
1. 傳遞中繼資料例項，可從以下網址取得： `TimeRangeCollection` 執行個體，到 `replaceCurrentItem` 方法(的一部分 `MediaPlayer` 介面)。
1. 等候TVSDK轉換為PREPARED狀態 `PlaybackEventListener#onPrepared` 要觸發的回呼。
1. 呼叫「 」以開始播放視訊 `play()` 方法(的一部分 `MediaPlayer` 介面)。

* 處理時間表衝突：在某些情況下 `TimeRange` 規格與播放時間軸重疊。 例如，與 `TimeRange` 規格可能低於已放置的結束位置值。 在此情況下，TVSDK會以無訊息方式調整違規專案的開始位置 `TimeRange` 避免時間表衝突的規格。 透過此調整，新的 `TimeRange` 會比原先指定的時間更短。 如果調整太過極端，以致於會導致 `TimeRange` 持續零毫秒，TVSDK會以無訊息方式捨棄違規專案 `TimeRange` 規格。

* 時間 `TimeRange` 提供自訂廣告插播的規格，TVSDK會嘗試將這些轉譯為分組在廣告插播內的廣告。 TVSDK會尋找相鄰的 `TimeRange` 規格並將它們叢集到個別的廣告插播中。 如果時間範圍與任何其他時間範圍都不相鄰，則會將其轉譯為包含單一廣告的廣告插播。

* 假設正在載入的媒體播放器專案指向VOD資產。 TVSDK會在您的應用程式嘗試載入中繼資料包含的媒體資源時檢查此專案 `TimeRange` 僅可在自訂廣告標籤功能內容中使用的規格。 如果基礎資產不是VOD型別，TVSDK程式庫會擲回例外狀況。

* 處理自訂廣告標籤時，TVSDK會停用其他廣告解決機制(透過Adobe Primetime ad decisioning （先前稱為Auditude）或其他廣告布建系統)。 您可以使用TVSDK提供的各種廣告解析程式模組之一，或是自訂廣告標籤機制。 使用自訂廣告標籤API時，會將廣告內容視為已解析並放置在時間軸上。

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

下列程式碼片段提供簡單範例，說明一組3個 `TimeRange` 規格會以自訂廣告標籤的形式放置在時間軸上。

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
