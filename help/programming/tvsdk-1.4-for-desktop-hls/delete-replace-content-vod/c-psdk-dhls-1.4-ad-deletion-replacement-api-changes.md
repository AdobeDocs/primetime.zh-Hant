---
description: TVSDK中的這些變更支援刪除和取代。
seo-description: TVSDK中的這些變更支援刪除和取代。
seo-title: 廣告刪除和取代API變更
title: 廣告刪除和取代API變更
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 廣告刪除和取代API變更 {#ad-deletion-and-replacement-api-changes}

TVSDK中的這些變更支援刪除和取代。

* `AdSignalingMode` 已新增 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  `extractAdSignalingMode()` -設 `AdSignalingMode.CUSTOM_RANGES` 定取代範圍是否在中繼資料中。

* `PlacementType` 已新增 `CUSTOM_RANGE` 類型。

* `PlacementMode`

   * 已新增 `DELETE` 模式。
   * 新增模 `MARK` 式
   * 添加模 `FreeReplace` 式——此模式具有持續時間，但是純插入

* `TimeRange` 不再是類 `final` 別

* 新增方 `ReplaceTimeRange()` 法

   延伸 `TimeRange` 至具有屬 `replacementDuration` 性。 對於MARK和DELETE案例， `replacementDuration` 為0。

* `TimeRangeCollection`

   * 已新增 `toReplaceMetadata()` 要擷取的公用程式功能 `timeRanges`。

   * 修改為使用 `DELETE` 和 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已新 `createCustomTimeRangesFrom()` 增——從JSON檔案建立MARK/DELETE/REPLACE使用案例的中繼資料。
   * 已移除 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 已新增 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 已新增 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未變更）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 新增 `CustomRangesOpportunityGenerator` 元資料包含自訂範圍的時間
   * `doRetrieveResolvers()`

      * 在元 `CustomRangeResolver` 資料中出現DELETE和REPLACE自訂範圍時新增
      * 領先 `CustomAdMarkerResolver` 於 `AuditudeResolver`


* 已新增 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空——無更新、VOD
   * `doProcess()` 建立新類型的新位置 `Placement.Delete_Range`

   * 在中 `CustomRangeOppotunityGenerator` 的生成器清單頂部添加了一個， `DefaultContentFactory`因此刪除範圍在廣告插入之前會處理。

   * 新增 `createCustomRangeOpportunities` 以建立所有商機

      MARK —— 每個有效標籤範圍的一個機 `PlacementType.CUSTOM_RANGE` 會 `PlacementMode.MARK`

      DELETE —— 每個有效刪除範圍和 `PlacementType.CUSTOM_RANGE``PlacementMode.DELETE`

      REPLACE —— 每個有效替換範圍有兩個機會：

      1. 和的刪除範圍 `PlacementType.CUSTOM_RANGE` 機會 `PlacementMode.DELETE`。

      1. Primetime廣告決策廣告機 `PlacementType.MID_ROLL` 會 `PlacementType.PRE_ROLL` 及 `PlacementMode.FREEREPLACE`

* 新增 `CustomRangeResolver`:

   * `doCanResolve()` 傳回 `true` 刪除範圍。

   * 已新 `createDeleteRangeOperation()` 增為 `DeleteRange` 位置建立

* 新增 `CustomRangeHelper`:

   * 用於提取標籤／刪除／替換並處理這些標籤的 `timeRanges` 公用程式類。
   * 已新增 `extractCustomRangesMetadata()`
   * 已新增 `extractCustomRanges()`
   * 添加 `mergeRanges()` -解決衝突和子集／合併

* `MediaPlayerTimeline`:

   * &quot;>在中 `executeOperation()`，如果操作是 `DeleteRange`，則在操作中添加對remove方法的調用

   * 在中 `executeOperation()`，如果操作是 `NOPTimelineOperation` (從服 `AdBreaks` 務器返回空的)，則添加要清除的調用。

   * 已新增 `onDeleteRangeComplete()`
   * 已新增 `removeRange()`
   * 在模 `adjustPlacement()`式中， `PlacementMode.FREEREPLACE` 將持續時間設為零。 請求時需要此持續時 `AdBreaks`間較早，此時需要為零才能完全插入。

* `VideoEngineTimeline` 新增 `removeC3Ad()` -呼叫 `removeByLocalTime()` 刪除範圍

* `AdSignalingModeGenerator`

   * `doConfigure()` -如果未生成任何機會，則不解決
   * `createInitialOpportunity()` -不要為生成初始機會 `AdSignalingMode.CUSTOM_RANGE`。 這 `CustomRangeOpportunityGenerator` 個已經蓋過了。

* `DeleteRange`

   * 延伸 `TimelineOperation`。
   * 建立者 `CustomRangeResolver` 用於刪除和替換（替換的刪除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` -允許裝箱
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 該 `accepts()` 方法經過修改，允許不同鋪放類型（前輥、中輥、後輥）的包裝

* `AuditudeRequestHelper` 允許伺服器覆寫廣告參數的錯誤修正

* `AuditudeResolver` 方 `canBePacked()` 法已變更為允許包裝

* `CustomAdResolver` 已 `timeRange` 移除擷取功能。 我們一次得到一個位置，然後把它變成一個 `AdBreakPlacement timelineOperation`。

