---
description: Android TVSDK API中的這些更改支援刪除和替換。
title: 廣告刪除和替換API更改
exl-id: bde8bd6e-0afe-42d0-b716-f33f75de757e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# 廣告刪除和替換API更改{#ad-deletion-and-replacement-api-changes}

Android TVSDK API中的這些更改支援刪除和替換。

* `AdSignalingMode` 新的自定義時間範圍和信令模式

* `AdvertisingMetadata` 新建 `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`:設定處理元資料時要標籤、刪除或替換的時間範圍

* `ContentResolver`

   * 新建 `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * 新建 `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* 新建 `ContentRemoval` 類

   `TimelineOperation` 定義要從時間軸中刪除的時間範圍的類

* `AuditudeResolver`

   * 新建 `private LinkedList<AuditudeRequest> _requestQueue`
   * 新建 `void startConsumer()`:開始處理黃金時段廣告決策請求隊列，並確保在 `MIN_INIT_REQUEST_INTERVAL` 間隔

   * 新建 `processReplacementRange()`:從廣告元資料中提取時間範圍並生成 `PlacementInformations`，並建立包含 `PlacementInformations`。

   * 新建 `canDoResolver()`:檢查放置機會是否具有黃金時段廣告決策元資料

* 新建 `CustomRangeHelper` 從ad元資料中提取時間範圍元資料並刪除子集/重疊/無效時間範圍的幫助程式類。

* 新建 `DeleteContentResolver` 解析內容解析器的放置機會 `PlacementInformation.Mode.DELETE`

* 新建 `NopTimelineOperation` 無需進行廣告中斷放置或替換時的新時間線操作。 此類用於區分此類和在解析過程中出現錯誤時。

* `TimelineOperationQueue` 檢查時間軸操作是否為 `NopTimelineOperation` 處理之前。

* `CustomAdMarkersContentResolver` 新建 `canDoResolve()`:檢查職位安排機會是否屬於類型 `Mode.MARK`

* `MetadataResolver` 新建 `canDoResolve()`:檢查職位安排機會是否屬於類型 `Mode.INSERT`

* `DefaultMetadataKeys` 新建 `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * 新模式 `enum (INSERT, DELETE, REPLACE, MARK)`
   * 新類型 `CUSTOM_TIME_RANGES`

* `TimeRange` 新建 `compareTo(TimeRange timeRange)`:因此，可以根據開始時間對TimeRanges排序

* 新建 `ReplacementTimeRange` 擴展 `TimeRange` 代表替換時間表的類， `begin`。 `end`, `replacement-duration` 的下界。

* `TimeRangeCollection`

   * 新建 `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * 已更名 `CUSTOM_AD_MARKERS` 至 `MARK_RANGES`

   * 已修改 `toMetadata(Metadata options)` 將刪除/標籤/替換範圍放入ad元資料。

* `MediaPlayerNotification`

   * 新建 `UNDEFINED_TIME_RANGES`:當ad信令模式是伺服器映射或清單提示時，並且替換範圍也在ad元資料中時，將忽略替換範圍。
   * 新建 `REPLACE_RANGES_NOT_AVAILABLE`:當ad信令模式為自定義時間範圍且替換範圍不可用時，將發出警告。

* `AdvertisingFactory` 新建 `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` 新建 `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` 新建 `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * 在 `prepareToPlay()`:將初始查找設定為0，因為如果範圍 `[0,n]` 刪除後，媒體播放器將不會自動播放。

   * 在 `prepareToPlay()`:循環瀏覽初始放置資訊清單 `mediaplayerclient` 來解決。

   * 在 `extractAdSignalingMode()`:適應新的自定義時間範圍模式。
   * 新建 `private static List<PlacementInformation> createInitalPlacementInformations()`:生成廣告信令模式和內容解析器（從廣告元資料導出）的初始放置資訊。
   * 在 `ContentPlacementCompletedListener`:檢查是否 `mediaPlayerClient` 是 `doneInitialResolving` 前 `endAdResolving`。

* `MediaPlayerClient`

   * 新建 `List<ContentResolver> _contentResolvers`
   * 新建 `int _reservations`
   * 新建 `lookupContentResolver(PlacementOpportunity placementOpportunity)`:查找哪些解析程式可以解析 `PlacementOpportunity`。

   * 修改的代碼以建立多個內容解析器。
   * 新建 `public boolean doneInitialResolving()`:檢查是否還有任何機會需要解決。

* `VideoEngineTimeline`

   * 新建 `removeContent(TimelineOperation timelineOperation)`:從時間軸中刪除給定的內容範圍。
   * 新建 `removeContentByLocalTime(long begin, long end)`:按給定的本地時間刪除內容 `begin` 和 `end`。

* `DefaultOpportunityDetectorFactory` 已修改 `createOpportunityDetector`:對於VOD流，僅返回新 `SpliceOutOpportunityDetector` 如果沒有MARK或REPLACE範圍（因為這些範圍比信令模式具有優先順序）。
