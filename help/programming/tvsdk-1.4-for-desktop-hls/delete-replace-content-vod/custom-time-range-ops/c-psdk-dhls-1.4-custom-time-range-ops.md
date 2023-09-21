---
description: TVSDK支援以程式設計方式刪除和取代VOD串流中的廣告內容。
title: 自訂時間範圍作業
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 概觀 {#custom-time-range-operations-overview}

TVSDK支援以程式設計方式刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為廣告相關內容期間。 除了標示這些時間範圍外，您也可以刪除和取代時間範圍。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

使用自訂標籤來實作廣告刪除和取代，這些標籤可識別VOD資料流中不同型別的時間範圍：標籤、刪除和取代。 對於每個自訂時間範圍，您可以執行關聯的操作，包括刪除或取代廣告內容。

對於廣告刪除和取代，TVSDK包含下列專案 *自訂時間範圍作業* 模式：

* 標籤 — 派單 `AdBreak` 已標籤區域的事件。 (這稱為 `customAdMarker` （在舊版TVSDK中）。 此模式不允許廣告插入。

* DELETE — 對於此模式，應用程式會使用 `TimeRangeCollection` 類別以定義C3廣告刪除的時間區域。 此模式允許廣告插入。
* REPLACE — 在此模式中，應用程式會取代 `timeRange` 搭配Adobe Primetime ad decisioning `AdBreak`. 取代操作會從C3廣告刪除發生處開始，並在指定的時間（比原始時間範圍短或長）結束。

TVSDK提供 `CustomRangesOpportunityGenerator` 類別來產生MARK和DELETE範圍的置入機會。 對於REPLACE模式，TVSDK會為每個時間範圍產生兩個放置機會：

* 此 `CustomRangeResolver` 產生DELETE的刊登機會
* 此 `AuditudeAdResolver` 產生INSERT的置入機會。
