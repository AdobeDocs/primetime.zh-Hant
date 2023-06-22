---
description: Android TVSDK API中的這些變更支援廣告刪除和取代。
title: 廣告刪除和取代API變更
exl-id: bde8bd6e-0afe-42d0-b716-f33f75de757e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# 廣告刪除和取代API變更{#ad-deletion-and-replacement-api-changes}

Android TVSDK API中的這些變更支援廣告刪除和取代。

* `AdSignalingMode` 新的自訂時間範圍和訊號模式

* `AdvertisingMetadata` 新增 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`：設定處理中繼資料時標籤、刪除或取代的時間範圍

* `ContentResolver`

   * 新增 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 新增 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 新增 `ContentRemoval` 類別

   `TimelineOperation` 定義要從時間軸移除的時間範圍的類別

* `AuditudeResolver`

   * 新增 `private LinkedList<AuditudeRequest> _requestQueue`
   * 新增 `void startConsumer()`：開始處理Primetime ad Decisioning請求佇列，並確保每個請求都是在 `MIN_INIT_REQUEST_INTERVAL` 間隔

   * 新增 `processReplacementRange()`：從廣告中繼資料擷取時間範圍並產生 `PlacementInformations`，並建立Primetime廣告決策請求，包含 `PlacementInformations`.

   * 新增 `canDoResolver()`：檢查刊登位置機會是否有Primetime廣告決策中繼資料

* 新增 `CustomRangeHelper` 從廣告中繼資料擷取時間範圍中繼資料，並移除子集/重疊/無效時間範圍的協助程式類別。

* 新增 `DeleteContentResolver` 解決以下位置機會的內容解析程式： `PlacementInformation.Mode.DELETE`

* 新增 `NopTimelineOperation` 新的時間表操作，適用於不需要進行廣告插播放置或取代的情況。 此類別用於區分此與解析過程中發生錯誤的時間。

* `TimelineOperationQueue` 檢查時間表作業是否為 `NopTimelineOperation` 處理之前。

* `CustomAdMarkersContentResolver` 新增 `canDoResolve()`：檢查刊登版位機會是否為型別 `Mode.MARK`

* `MetadataResolver` 新增 `canDoResolve()`：檢查刊登版位機會是否為型別 `Mode.INSERT`

* `DefaultMetadataKeys` 新增 `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 新模式 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 新型別 `CUSTOM_TIME_RANGES`

* `TimeRange` 新增 `compareTo(TimeRange timeRange)`：依開始時間排序時間範圍同樣有效

* 新增 `ReplacementTimeRange` 擴充 `TimeRange` 代表取代時間範圍的類別，使用 `begin`， `end`、和 `replacement-duration` 引數。

* `TimeRangeCollection`

   * 新增 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 已重新命名 `CUSTOM_AD_MARKERS` 至 `MARK_RANGES`

   * 修改時間 `toMetadata(Metadata options)` 將刪除/標籤/取代範圍放入廣告中繼資料。

* `MediaPlayerNotification`

   * 新增 `UNDEFINED_TIME_RANGES`：當廣告訊號模式為伺服器對應或資訊清單提示，且取代範圍也在廣告中繼資料中時，取代範圍會遭到忽略。
   * 新增 `REPLACE_RANGES_NOT_AVAILABLE`：當廣告訊號模式為自訂時間範圍且取代範圍無法使用時，將會傳送警告。

* `AdvertisingFactory` 新增 `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 新增 `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 新增 `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 在 `prepareToPlay()`：將初始搜尋設為0，因為若為範圍 `[0,n]` 刪除，媒體播放器將不會自動播放。

   * 在 `prepareToPlay()`：在初始位置資訊清單中循環 `mediaplayerclient` 以解決。

   * 在 `extractAdSignalingMode()`：適應新的自訂時間範圍模式。
   * 新增 `private static List<PlacementInformation> createInitalPlacementInformations()`：產生廣告訊號模式和內容解析器的初始位置資訊（衍生自廣告中繼資料）。
   * 在 `ContentPlacementCompletedListener`：檢查以檢視 `mediaPlayerClient` 是 `doneInitialResolving` 呼叫前 `endAdResolving`.

* `MediaPlayerClient`

   * 新增 `List<ContentResolver> _contentResolvers`
   * 新增 `int _reservations`
   * 新增 `lookupContentResolver(PlacementOpportunity placementOpportunity)`：查詢哪個解析器可以解析 `PlacementOpportunity`.

   * 修改程式碼以建立多個內容解析器。
   * 新增 `public boolean doneInitialResolving()`：檢查是否有任何機會需要解決。

* `VideoEngineTimeline`

   * 新增 `removeContent(TimelineOperation timelineOperation)`：從時間軸移除指定的內容範圍。
   * 新增 `removeContentByLocalTime(long begin, long end)`：依指定的當地時間移除內容 `begin` 和 `end`.

* `DefaultOpportunityDetectorFactory` 修改時間 `createOpportunityDetector`：針對VOD資料流，只會傳回新的 `SpliceOutOpportunityDetector` 如果沒有MARK或REPLACE範圍（因為這些範圍優先於訊號模式）。
