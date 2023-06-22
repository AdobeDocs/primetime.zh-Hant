---
description: TVSDK支援程式化地刪除和取代VOD串流中的廣告內容。
title: 自訂時間範圍作業
exl-id: 5480b22a-ecff-4fd8-9ec0-40e4a2e97641
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 概觀 {#custom-time-range-operations-overview}

TVSDK支援程式化地刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為與廣告相關的內容句號。 除了標示這些時間範圍外，您也可以刪除和取代時間範圍。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

使用自訂標籤來實施廣告刪除和取代，這些標籤可識別VOD資料流中不同型別的時間範圍：標籤、刪除和取代。 對於每個自訂時間範圍，您可以執行關聯的操作，包括刪除或取代廣告內容。

對於廣告刪除和取代，TVSDK包含下列專案 *自訂時間範圍作業* 模式：

* 標籤 — 派單 `AdBreak` 標籤區域的事件。 (這稱為 `customAdMarker` （在舊版TVSDK中）。 此模式不允許廣告插入。

* DELETE — 對於此模式，應用程式會使用 `TimeRangeCollection` 類別，定義C3廣告刪除的時間區域。 此模式允許廣告插入。
* REPLACE — 在此模式中，應用程式會取代 `timeRange` 搭配Adobe Primetime ad decisioning `AdBreak`. 取代操作從C3廣告刪除發生處開始，並在指定的時間（比原始時間範圍短或長）結束。

TVSDK提供 `CustomRangesOpportunityGenerator` 類別來產生MARK和DELETE範圍的置入機會。 對於REPLACE模式，TVSDK會為每個時間範圍產生兩個置入機會：

* 此 `CustomRangeResolver` 產生DELETE的投放機會
* 此 `AuditudeAdResolver` 為INSERT產生置入機會。
