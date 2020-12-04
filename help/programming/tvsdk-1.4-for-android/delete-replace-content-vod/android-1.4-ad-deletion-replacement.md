---
description: 這些Android TVSDK API中的變更支援刪除和取代廣告。
seo-description: 這些Android TVSDK API中的變更支援刪除和取代廣告。
seo-title: 廣告刪除和取代API變更
title: 廣告刪除和取代API變更
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# 廣告刪除和取代API變更{#ad-deletion-and-replacement-api-changes}

這些Android TVSDK API中的變更支援刪除和取代廣告。

* `AdSignalingMode` 新的自訂時間範圍廣告信令模式

* `AdvertisingMetadata` 新功 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`能：設定處理中繼資料時要標籤、刪除或取代的時間範圍

* `ContentResolver`

   * 新`public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 新`protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 新`ContentRemoval`類別

   `TimelineOperation` 定義要從時間軸中刪除的時間範圍的類

* `AuditudeResolver`

   * 新`private LinkedList<AuditudeRequest> _requestQueue`
   * 新`void startConsumer()`:開始處理Primetime廣告決策請求佇列，並確保每個請求以`MIN_INIT_REQUEST_INTERVAL`間隔發出

   * 新`processReplacementRange()`:從廣告中繼資料擷取時間範圍並產生`PlacementInformations`，並建立包含`PlacementInformations`的Primetime廣告決策請求。

   * 新`canDoResolver()`:檢查位置商機是否有Primetime廣告決策中繼資料

* 新的`CustomRangeHelper` Helper類別，可從廣告中繼資料擷取時間範圍中繼資料，並移除子集／重疊／無效的時間範圍。

* 新的`DeleteContentResolver`內容解析程式，可解決`PlacementInformation.Mode.DELETE`的放置機會

* 新`NopTimelineOperation`新時間軸作業，適用於不需要進行廣告插播位置或取代的時間軸作業。 此類用於區分這類和解析過程中出現錯誤時。

* `TimelineOperationQueue` 在處理前檢查時間軸操 `NopTimelineOperation` 作是否為。

* `CustomAdMarkersContentResolver` 新功 `canDoResolve()`能：檢查職位安排機會是否為類型  `Mode.MARK`

* `MetadataResolver` 新功 `canDoResolve()`能：檢查職位安排機會是否為類型  `Mode.INSERT`

* `DefaultMetadataKeys` 新增  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 新模式`enum (INSERT, DELETE, REPLACE, MARK)`
   * 新類型`CUSTOM_TIME_RANGES`

* `TimeRange` 新功 `compareTo(TimeRange timeRange)`能：因此，可以根據開始時間對時間範圍進行排序

* 新`ReplacementTimeRange`使用`begin`、`end`和`replacement-duration`參數擴充代表替換時間範圍的`TimeRange`類別。

* `TimeRangeCollection`

   * 新`MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 將`CUSTOM_AD_MARKERS`重新命名為`MARK_RANGES`

   * 已修改`toMetadata(Metadata options)`，將刪除／標籤／取代範圍放入廣告中繼資料。

* `MediaPlayerNotification`

   * 新`UNDEFINED_TIME_RANGES`:當廣告信令模式是伺服器地圖或資訊清單提示，且取代範圍也在廣告中繼資料中時，取代範圍會被忽略。
   * 新`REPLACE_RANGES_NOT_AVAILABLE`:當廣告信令模式為「自訂時間範圍」且無法使用取代範圍時，將會傳送警告。

* `AdvertisingFactory` 新增  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 新增  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 新增  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 在`prepareToPlay()`中：將初始搜尋設為0，因為如果刪除範圍`[0,n]`，媒體播放器將不會自動播放。

   * 在`prepareToPlay()`中：循環查看`mediaplayerclient`要解決的初始放置資訊清單。

   * 在`extractAdSignalingMode()`中：適應新的自訂時間範圍模式。
   * 新`private static List<PlacementInformation> createInitalPlacementInformations()`:生成廣告信令模式和內容解析器的初始放置資訊（從廣告元資料衍生）。
   * 在`ContentPlacementCompletedListener`中：在呼叫`endAdResolving`之前，檢查`mediaPlayerClient`是否為`doneInitialResolving`。

* `MediaPlayerClient`

   * 新`List<ContentResolver> _contentResolvers`
   * 新`int _reservations`
   * 新`lookupContentResolver(PlacementOpportunity placementOpportunity)`:查找哪個解析程式可以解析`PlacementOpportunity`。

   * 已修改程式碼以建立多個內容解析器。
   * 新`public boolean doneInitialResolving()`:檢查是否還有任何機會有待解決。

* `VideoEngineTimeline`

   * 新`removeContent(TimelineOperation timelineOperation)`:從時間軸移除指定範圍的內容。
   * 新`removeContentByLocalTime(long begin, long end)`:移除`begin`和`end`的本機時間內容。

* `DefaultOpportunityDetectorFactory` 已修 `createOpportunityDetector`改：對於VOD串流，只有在沒有MARK或REPLACE `SpliceOutOpportunityDetector` 範圍時（因為這些範圍比信令模式具有優先順序）才返回新的。

