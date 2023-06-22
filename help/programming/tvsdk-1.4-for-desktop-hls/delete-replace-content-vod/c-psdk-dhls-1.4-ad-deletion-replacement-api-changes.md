---
description: TVSDK中的這些變更支援廣告刪除和取代。
title: 廣告刪除和取代API變更
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 廣告刪除和取代API變更 {#ad-deletion-and-replacement-api-changes}

TVSDK中的這些變更支援廣告刪除和取代。

* `AdSignalingMode` 已新增 `CUSTOM_RANGES` 訊號模式。

* `OpportunityGenerator`  `extractAdSignalingMode()`  — 設定 `AdSignalingMode.CUSTOM_RANGES` 如果取代範圍在中繼資料中。

* `PlacementType` 已新增 `CUSTOM_RANGE` 型別。

* `PlacementMode`

   * 已新增 `DELETE` 模式。
   * 已新增 `MARK` 模式
   * 已新增 `FreeReplace` mode — 此模式有持續時間，但純為插入

* `TimeRange` 不再是 `final` 類別

* 已新增 `ReplaceTimeRange()` 方法

   延伸 `TimeRange` 以擁有 `replacementDuration` 屬性。 對於MARK和DELETE案例， `replacementDuration` 為0。

* `TimeRangeCollection`

   * 已新增 `toReplaceMetadata()` 要擷取的公用程式函式 `timeRanges`.

   * 已修改以使用 `DELETE` 和 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已新增 `createCustomTimeRangesFrom()`  — 從JSON檔案建立MARK/DELETE/REPLACE使用案例的中繼資料。
   * 已移除 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 已新增 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 已新增 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未變更）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 已新增 `CustomRangesOpportunityGenerator` 當中繼資料包含自訂範圍時為
   * `doRetrieveResolvers()`

      * 新增 `CustomRangeResolver` 適用於中繼資料中有DELETE和REPLACE自訂範圍的情況
      * 已移動 `CustomAdMarkerResolver` 超前 `AuditudeResolver`


* 已新增 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空 — 無更新、VOD
   * `doProcess()` 建立新型別的新位置 `Placement.Delete_Range`

   * 已新增 `CustomRangeOppotunityGenerator` 至產生器清單頂端 `DefaultContentFactory`，刪除範圍就會在廣告插入前處理。

   * 已新增 `createCustomRangeOpportunities` 以建立所有商機

      MARK — 每個有效的標籤範圍有一個機會 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.MARK`

      DELETE — 每個有效的刪除範圍一個機會 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`

      REPLACE — 每個有效取代範圍有兩個機會：

      1. 刪除範圍商機 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`.

      1. Primetime廣告決策廣告商機 `PlacementType.MID_ROLL` 或 `PlacementType.PRE_ROLL` 和 `PlacementMode.FREEREPLACE`

* 已新增 `CustomRangeResolver`：

   * `doCanResolve()` 傳回 `true` 刪除範圍。

   * 已新增 `createDeleteRangeOperation()` 建立 `DeleteRange` 放置

* 已新增 `CustomRangeHelper`：

   * 用於擷取「標籤/刪除/取代」的通用公用程式類別 `timeRanges` 並加以處理。
   * 已新增 `extractCustomRangesMetadata()`
   * 已新增 `extractCustomRanges()`
   * 已新增 `mergeRanges()`  — 解決衝突和子集/合併

* `MediaPlayerTimeline`:

   * 「>In `executeOperation()`，如果作業為 `DeleteRange`，在操作中新增了移除方法的呼叫

   * 在 `executeOperation()`，如果作業為 `NOPTimelineOperation` (空白 `AdBreaks` （從伺服器回來），新增要清除的呼叫。

   * 已新增 `onDeleteRangeComplete()`
   * 已新增 `removeRange()`
   * 在 `adjustPlacement()`，代表 `PlacementMode.FREEREPLACE` 模式，將持續時間清零。 請求時較先需要此持續時間 `AdBreaks`，此時，它必須是零才能純粹插入。

* `VideoEngineTimeline` 已新增 `removeC3Ad()`  — 呼叫 `removeByLocalTime()` 用於刪除範圍

* `AdSignalingModeGenerator`

   * `doConfigure()`  — 如果未產生商機，則不解析
   * `createInitialOpportunity()`  — 不要為以下專案產生初始機會 `AdSignalingMode.CUSTOM_RANGE`. 此 `CustomRangeOpportunityGenerator` 已涵蓋此內容。

* `DeleteRange`

   * 延伸 `TimelineOperation`.
   * 建立者 `CustomRangeResolver` 刪除和取代（取代的刪除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5`  — 允許包裝
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 此 `accepts()` 修改了方法，允許封裝不同的放置型別（前段、中段、後段）

* `AuditudeRequestHelper` 允許伺服器覆寫廣告引數的錯誤修正

* `AuditudeResolver` 此 `canBePacked()` 方法已變更為允許包裝

* `CustomAdResolver` 此 `timeRange` 擷取函式已移除。 我們一次會得到一個位置，然後將其轉換為 `AdBreakPlacement timelineOperation`.
