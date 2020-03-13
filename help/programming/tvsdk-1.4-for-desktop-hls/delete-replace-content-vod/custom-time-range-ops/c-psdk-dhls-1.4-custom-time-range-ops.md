---
description: TVSDK支援程式化刪除和取代VOD串流中的廣告內容。
seo-description: TVSDK支援程式化刪除和取代VOD串流中的廣告內容。
seo-title: 自訂時間範圍作業
title: 自訂時間範圍作業
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概觀 {#custom-time-range-operations-overview}

TVSDK支援程式化刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為廣告相關內容句點。 除了標籤這些時間範圍外，您也可以刪除和取代時間範圍。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

廣告刪除和取代是使用自訂標籤來實作，這些標籤可識別VOD串流中不同類型的時間範圍：標籤、刪除和替換。 您可以針對每個自訂時間範圍執行相關作業，包括刪除或取代廣告內容。

對於廣告刪除和取代，TVSDK包含下列自訂 *時間範圍作業模* 式：

* MARK —— 為已標籤 `AdBreak` 的區域調度事件。 (在舊版TVSDK `customAdMarker` 中已呼叫此功能)。此模式不允許廣告插入。

* DELETE —— 在此模式中，應用程式會使用 `TimeRangeCollection` 類別來定義C3廣告刪除的時間區域。 此模式允許廣告插入。
* 取代——在此模式中，應用程式會以Adobe Primetime `timeRange` 廣告決策取代廣告 `AdBreak`。 替換操作從C3廣告刪除發生的位置開始，並在指定時間（比原始時間範圍短或長）結束。

TVSDK提供類 `CustomRangesOpportunityGenerator` 別，以產生MARK和DELETE範圍的位置機會。 對於REPLACE模式，TVSDK會針對每個時間範圍產生兩個位置機會：

* 為DELETE `CustomRangeResolver` 生成位置機會
* 為INSERT `AuditudeAdResolver` 生成位置機會。