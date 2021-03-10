---
description: TVSDK中的這些變更支援刪除和取代。
title: 廣告刪除和取代API變更
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 廣告刪除和取代API變更{#ad-deletion-and-replacement-api-changes}

TVSDK中的這些變更支援刪除和取代。

* `AdSignalingMode` 已新增 `CUSTOM_RANGES` 信令模式。

* `OpportunityGenerator`  `extractAdSignalingMode()` -設定 `AdSignalingMode.CUSTOM_RANGES` 取代範圍是否在中繼資料中。

* `PlacementType` 已新增 `CUSTOM_RANGE` 類型。

* `PlacementMode`

   * 已新增`DELETE`模式。
   * 新增`MARK`模式
   * 已添加`FreeReplace`模式——此模式具有持續時間，但是純插入

* `TimeRange` 不再是類 `final` 別

* 已新增`ReplaceTimeRange()`方法

   將`TimeRange`擴展為具有`replacementDuration`屬性。 對於MARK和DELETE案例，`replacementDuration`為0。

* `TimeRangeCollection`

   * 已添加`toReplaceMetadata()`實用程式函式以提取`timeRanges`。

   * 已修改為與`DELETE`和`REPLACE`一起使用

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * 已新增`createCustomTimeRangesFrom()` —— 從JSON檔案建立MARK/DELETE/REPLACE使用案例的中繼資料。
   * 已移除`createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * 新增`CUSTOM_DELETE_RANGES_METADATA_KEY`
   * 新增`CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` （未變更）

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * 新增`CustomRangesOpportunityGenerator`，以用於中繼資料包含自訂範圍時
   * `doRetrieveResolvers()`

      * 新增`CustomRangeResolver`，以在中繼資料中出現DELETE和REPLACE自訂範圍時
      * 已將`CustomAdMarkerResolver`移至`AuditudeResolver`前面


* 新增`CustomRangeOpportunityGenerator`

   * `doUpdate()` 留空——無更新、VOD
   * `doProcess()` 建立新類型的新位置  `Placement.Delete_Range`

   * 將`CustomRangeOppotunityGenerator`新增至`DefaultContentFactory`中產生器清單的頂端，因此在廣告插入之前會處理刪除範圍。

   * 已新增`createCustomRangeOpportunities`以建立所有商機

      MARK —— 每個有效標籤範圍`PlacementType.CUSTOM_RANGE`和`PlacementMode.MARK`只有一個機會

      DELETE-每個有效刪除範圍`PlacementType.CUSTOM_RANGE`和`PlacementMode.DELETE`的一個機會

      REPLACE —— 每個有效替換範圍有兩個機會：

      1. `PlacementType.CUSTOM_RANGE`和`PlacementMode.DELETE`的刪除範圍機會。

      1. Primetime廣告決策廣告機會`PlacementType.MID_ROLL`或`PlacementType.PRE_ROLL`和`PlacementMode.FREEREPLACE`

* 新增`CustomRangeResolver`:

   * `doCanResolve()` 返回 `true` 刪除範圍。

   * 已新增`createDeleteRangeOperation()`以建立`DeleteRange`的位置

* 新增`CustomRangeHelper`:

   * 用於提取標籤／刪除／替換`timeRanges`並處理它們的通用實用程式類。
   * 新增`extractCustomRangesMetadata()`
   * 新增`extractCustomRanges()`
   * 添加`mergeRanges()` —— 解決衝突和子集／合併

* `MediaPlayerTimeline`:

   * &quot;>在`executeOperation()`中，如果操作為`DeleteRange`，則在操作中添加對remove方法的調用

   * 在`executeOperation()`中，如果操作是`NOPTimelineOperation`（從伺服器返回的空`AdBreaks`），則添加要清除的調用。

   * 新增`onDeleteRangeComplete()`
   * 新增`removeRange()`
   * 在`adjustPlacement()`中，對於`PlacementMode.FREEREPLACE`模式，將持續時間設為零。 在請求`AdBreaks`時，此持續時間較早，此時需要為零才能進行純插入。

* `VideoEngineTimeline` 已新 `removeC3Ad()` 增——呼 `removeByLocalTime()` 叫刪除範圍

* `AdSignalingModeGenerator`

   * `doConfigure()` -如果未生成任何機會，則不解決
   * `createInitialOpportunity()` -不要為生成初始機會 `AdSignalingMode.CUSTOM_RANGE`。`CustomRangeOpportunityGenerator`已涵蓋此問題。

* `DeleteRange`

   * 延伸`TimelineOperation`。
   * 由`CustomRangeResolver`建立，用於刪除和取代（取代的刪除部分）

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` -允許裝箱
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` 該 `accepts()` 方法經過修改，允許不同鋪放類型（前輥、中輥、後輥）的包裝

* `AuditudeRequestHelper` 允許伺服器覆寫廣告參數的錯誤修正

* `AuditudeResolver` 方 `canBePacked()` 法已變更為允許包裝

* `CustomAdResolver` 已 `timeRange` 移除擷取功能。我們一次得到一個位置，然後將它變成`AdBreakPlacement timelineOperation`。

