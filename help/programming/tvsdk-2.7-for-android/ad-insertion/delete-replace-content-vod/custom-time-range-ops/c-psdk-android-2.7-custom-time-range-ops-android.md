---
description: CustomRangeMetadata類標識VOD流標籤、刪除和替換中的不同類型的時間範圍。 對於這些自定義時間範圍類型中的每種類型，可以執行相應的操作，包括刪除和替換廣告內容。
title: 自定義時間範圍操作
exl-id: 52d2bbf6-107d-4e38-93ea-a29c9dd8c81e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 概述 {#custom-time-range-operations}

CustomRangeMetadata類標識VOD流中不同類型的時間範圍：標籤、刪除和替換。 對於這些自定義時間範圍類型中的每種類型，可以執行相應的操作，包括刪除和替換廣告內容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

對於廣告刪除和替換，TVSDK使用以下 *自定義時間範圍操作* 模式：

* **標籤** 此模式在TVSDK的早期版本中稱為自定義廣告標籤。 該模式標籤已被放入VOD流中的廣告的開始和結束時間。 當存在類型的時間範圍標籤時 `MARK` 在溪流中 `Mode.MARK` 生成者 `CustomMarkerOpportunityGenerator` 由 `CustomRangeResolver`。 未插入廣告。

* **DELETE** 對於 `DELETE` 時間範圍，初始 `placementInformation` 類型 `Mode.DELETE` 建立和解析時 `CustomRangeResolver`。 `DeleteRangeTimelineOperation` 定義要從時間軸中刪除的範圍，TVSDK使用 `removeByLocalTime` 從Adobe視頻引擎(AVE)API完成此操作。 如果存在DELETE範圍和Adobe Primetime和決策元資料，則首先刪除該範圍，然後 `AuditudeResolver` 使用典型的Adobe Primetime廣告決策工作流解析廣告。

* **替換** 對於 `REPLACE` 時間範圍，兩個初始 `placementInformations` 建立，一個 `Mode.DELETE` 一個 `Mode.REPLACE`。 `CustomRangeResolver` 先刪除時間範圍，然後刪除 `AuditudeResolver` 插入指定廣告 `replaceDuration` 進入時間軸。 否 `replaceDuration` 指定時，伺服器將確定插入的內容。

為支援這些自定義時間範圍操作，TVSDK提供了以下功能：

* 多個內容解析器

   流可以基於廣告信令模式和廣告元資料具有多個內容解析器。 行為隨著廣告信令模式和廣告元資料的不同組合而改變。
* 使用 `CustomMarkerOpportunityGenerator`。
* 一種新的廣告信號方式， `CUSTOM_RANGES`。

   廣告是基於來自外部源（如JSON檔案）的時間範圍資料進行放置的。
