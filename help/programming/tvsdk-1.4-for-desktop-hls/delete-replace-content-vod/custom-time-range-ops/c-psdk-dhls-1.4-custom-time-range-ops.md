---
description: TVSDK支援VOD流中廣告內容的寫程式刪除和替換。
title: 自定義時間範圍操作
exl-id: 5480b22a-ecff-4fd8-9ec0-40e4a2e97641
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 概述 {#custom-time-range-operations-overview}

TVSDK支援VOD流中廣告內容的寫程式刪除和替換。

刪除和替換特徵擴展了自定義和標籤特徵。 自定義廣告標籤將主內容的節標籤為與廣告相關的內容句點。 除了標籤這些時間範圍外，還可以刪除和替換時間範圍。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

廣告的刪除和替換是使用識別VOD流中不同類型的時間範圍的定製標籤來實現的：標籤、刪除和替換。 對於每個自定義時間範圍，您可以執行相關操作，包括刪除或替換廣告內容。

對於廣告刪除和替換，TVSDK包括以下內容 *自定義時間範圍操作* 模式：

* MARK — 派單 `AdBreak` 標籤區域的事件。 (這稱為 `customAdMarker` TVSDK的早期版本。) 在此模式下不允許插入廣告。

* DELETE — 對於此模式，應用使用 `TimeRangeCollection` 類以定義C3廣告刪除的時間區。 此模式允許插入廣告。
* REPLACE — 在此模式下，應用程式將替換 `timeRange` Adobe Primetime和決定 `AdBreak`。 替換操作從C3 Ad刪除發生的位置開始，並在指示的時間（比原始時間範圍短或長）結束。

TVSDK提供 `CustomRangesOpportunityGenerator` 類，為MARK和DELETE範圍生成放置機會。 對於REPLACE模式，TVSDK為每個時間範圍生成兩個放置機會：

* 的 `CustomRangeResolver` 為DELETE生成職位安排機會
* 的 `AuditudeAdResolver` 為INSERT生成放置機會。
