---
description: TVSDK支援程式化刪除和取代VOD串流中的廣告內容。
title: 自訂時間範圍作業
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 概述{#custom-time-range-operations-overview}

TVSDK支援程式化刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為廣告相關內容句點。 除了標籤這些時間範圍外，您也可以刪除和取代時間範圍。

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

廣告刪除和取代是使用自訂標籤來實作，這些標籤可識別VOD串流中不同類型的時間範圍：標籤、刪除和替換。 您可以針對每個自訂時間範圍執行相關作業，包括刪除或取代廣告內容。

對於廣告刪除和取代，TVSDK包含下列&#x200B;*自訂時間範圍作業*&#x200B;模式：

* MARK —— 為標籤區域調度`AdBreak`事件。 （在舊版TVSDK中，此名稱稱為`customAdMarker`。） 此模式不允許廣告插入。

* DELETE-在此模式中，應用程式會使用`TimeRangeCollection`類別來定義C3廣告刪除的時間區域。 此模式允許廣告插入。
* REPLACE —— 在此模式中，應用程式會以Adobe Primetime廣告決策`AdBreak`取代`timeRange`。 替換操作從C3廣告刪除發生的位置開始，並在指定時間（比原始時間範圍短或長）結束。

TVSDK提供`CustomRangesOpportunityGenerator`類別，以產生MARK和DELETE範圍的放置機會。 對於REPLACE模式，TVSDK會針對每個時間範圍產生兩個位置機會：

* `CustomRangeResolver`會產生DELETE的放置機會
* `AuditudeAdResolver`為INSERT生成放置機會。