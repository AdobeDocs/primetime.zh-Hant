---
description: CustomRangeMetadata類別可識別VOD串流標籤、刪除和取代中不同類型的時間範圍。 對於這些自訂時間範圍類型，您可以執行相應的作業，包括刪除和取代廣告內容。
seo-description: CustomRangeMetadata類別可識別VOD串流標籤、刪除和取代中不同類型的時間範圍。 對於這些自訂時間範圍類型，您可以執行相應的作業，包括刪除和取代廣告內容。
seo-title: 自訂時間範圍作業
title: 自訂時間範圍作業
uuid: e9c6a135-124e-44d4-adf2-dc9d671e2483
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 概觀 {#custom-time-range-operations}

CustomRangeMetadata類別可識別VOD串流中不同類型的時間範圍：標籤、刪除和替換。 對於這些自訂時間範圍類型，您可以執行相應的作業，包括刪除和取代廣告內容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

對於廣告刪除和取代，TVSDK使用下列自訂時 *間範圍作業模* 式：

* **MARK** This mode is recorded to custom ad markers in verious of TVSDK. 此模式會標示已置入VOD串流之廣告的開始和結束時間。 當串流中有時間範圍標籤 `MARK` 類型時，由產生並解 `Mode.MARK` 決初始 `CustomMarkerOpportunityGenerator` 放置問題 `CustomRangeResolver`。 不會插入廣告。

* **DELETE** （刪除） `DELETE` 對於時間範圍，會 `placementInformation` 由建立並 `Mode.DELETE` 解決初始類型 `CustomRangeResolver`。 `DeleteRangeTimelineOperation` 定義要從時間軸移除的範圍，而TVSDK `removeByLocalTime` 則使用Adobe視訊引擎(AVE)API來完成此作業。 如果有DELETE範圍和Adobe Primetime廣告決策中繼資料，則先刪除範圍，然後使用典型的Adobe Primetime廣告決策工作流程 `AuditudeResolver` 來解析廣告。

* **REPLACE** 對於 `REPLACE` 時間範圍，會建立兩個 `placementInformations` 初始值，一個 `Mode.DELETE` 和一個 `Mode.REPLACE`。 `CustomRangeResolver` 先刪除時間範圍，然後將指 `AuditudeResolver` 定的廣告插入 `replaceDuration` 時間軸。 如果未指 `replaceDuration` 定，則伺服器將決定要插入的內容。

為支援這些自訂時間範圍作業，TVSDK提供下列功能：

* 多種內容解析器

   流可以基於廣告信令模式和廣告元資料具有多個內容解析器。 行為會隨著廣告信號模式和廣告中繼資料的不同組合而改變。
* 使用多個初始商 `CustomMarkerOpportunityGenerator`機。
* 新的廣告信令模式， `CUSTOM_RANGES`。

   廣告會根據來自外部來源（例如JSON檔案）的「時間範圍」資料來放置。

