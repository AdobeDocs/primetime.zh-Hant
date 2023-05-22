---
description: TVSDK中的這些更改支援刪除和替換。
title: 廣告刪除和替換API更改
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 廣告刪除和替換API更改 {#ad-deletion-and-replacement-api-changes}

TVSDK中的這些更改支援刪除和替換。

* `AdSignalingMode` 已添加 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  `extractAdSignalingMode()`  — 設定 `AdSignalingMode.CUSTOM_RANGES` 元資料中是否包含替換區域。

* `PlacementType` 已添加 `CUSTOM_RANGE` 的雙曲餘切值。

* `PlacementMode`

   * 已添加 `DELETE` 的子菜單。
   * 已添加 `MARK` 模式
   * 已添加 `FreeReplace` 模式 — 此模式具有持續時間，但是是純插入

* `TimeRange` 不再是 `final` 類

* 已添加 `ReplaceTimeRange()` 方法

   擴展 `TimeRange` 要 `replacementDuration` 屬性。 對於MARK和DELETE案， `replacementDuration` 為0。

* `TimeRangeCollection`

   * 已添加 `toReplaceMetadata()` 實用函式提取 `timeRanges`。

   * 修改為使用 `DELETE` 和 `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已添加 `createCustomTimeRangesFrom()`  — 從JSON檔案為MARK/DELETE/REPLACE使用案例建立元資料。
   * 已刪除 `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 已添加 `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 已添加 `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未更改）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 已添加 `CustomRangesOpportunityGenerator` 當元資料包含自定義範圍時
   * `doRetrieveResolvers()`

      * 添加 `CustomRangeResolver` 當元資料中存在DELETE和REPLACE自定義範圍時
      * 已移動 `CustomAdMarkerResolver` 前 `AuditudeResolver`


* 已添加 `CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空 — 無更新，VOD
   * `doProcess()` 建立新類型的新放置 `Placement.Delete_Range`

   * 已添加 `CustomRangeOppotunityGenerator` 到生成器清單的頂部 `DefaultContentFactory`，因此在插入廣告之前會處理刪除範圍。

   * 已添加 `createCustomRangeOpportunities` 創造所有機會

      MARK — 每個有效標籤範圍的一個機會 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.MARK`

      DELETE — 每個有效刪除範圍的一個機會 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`

      REPLACE — 每個有效替換範圍的兩個機會：

      1. 刪除範圍的機會 `PlacementType.CUSTOM_RANGE` 和 `PlacementMode.DELETE`。

      1. 黃金時段廣告的決策與機遇 `PlacementType.MID_ROLL` 或 `PlacementType.PRE_ROLL` 和 `PlacementMode.FREEREPLACE`

* 已添加 `CustomRangeResolver`:

   * `doCanResolve()` 返回 `true` 的子菜單。

   * 已添加 `createDeleteRangeOperation()` 建立 `DeleteRange` 的

* 已添加 `CustomRangeHelper`:

   * 用於提取標籤/刪除/替換的公用實用程式類 `timeRanges` 並處理它們。
   * 已添加 `extractCustomRangesMetadata()`
   * 已添加 `extractCustomRanges()`
   * 已添加 `mergeRanges()`  — 解決衝突和子集/合併

* `MediaPlayerTimeline`:

   * &quot;>在 `executeOperation()`，則 `DeleteRange`，在操作中添加了要刪除的調用

   * 在 `executeOperation()`，則 `NOPTimelineOperation` （空） `AdBreaks` 從伺服器返回)，添加呼叫以清除。

   * 已添加 `onDeleteRangeComplete()`
   * 已添加 `removeRange()`
   * 在 `adjustPlacement()`, `PlacementMode.FREEREPLACE` 模式，將持續時間歸零。 請求時，需要提前提供此持續時間 `AdBreaks`，此時需要為0才能為純插入。

* `VideoEngineTimeline` 已添加 `removeC3Ad()`  — 呼叫 `removeByLocalTime()` 刪除範圍

* `AdSignalingModeGenerator`

   * `doConfigure()`  — 如果未生成任何機會，則不解決
   * `createInitialOpportunity()`  — 不為 `AdSignalingMode.CUSTOM_RANGE`。 的 `CustomRangeOpportunityGenerator` 已經涵蓋了。

* `DeleteRange`

   * 擴展 `TimelineOperation`。
   * 建立者 `CustomRangeResolver` 刪除和替換（替換的刪除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5`  — 允許裝箱
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 的 `accepts()` 修改了方法以允許不同放置類型（預卷、中卷、後卷）的包裝

* `AuditudeRequestHelper` 錯誤修復允許伺服器覆蓋Ad參數

* `AuditudeResolver` 的 `canBePacked()` 方法更改為允許包裝

* `CustomAdResolver` 的 `timeRange` 已刪除抽取函式。 我們一次得到一個職位，然後 `AdBreakPlacement timelineOperation`。
