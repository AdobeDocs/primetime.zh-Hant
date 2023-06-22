---
description: CustomRangeMetadata類別會識別VOD資料流標籤、刪除和取代中不同型別的時間範圍。 對於每種自訂時間範圍型別，您可以執行對應的操作，包括刪除和取代廣告內容。
title: 自訂時間範圍作業
exl-id: 52d2bbf6-107d-4e38-93ea-a29c9dd8c81e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 概觀 {#custom-time-range-operations}

CustomRangeMetadata類別會識別VOD資料流中不同型別的時間範圍：標籤、刪除和取代。 對於每種自訂時間範圍型別，您可以執行對應的操作，包括刪除和取代廣告內容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

對於廣告刪除和取代，TVSDK會使用下列專案 *自訂時間範圍作業* 模式：

* **標籤** 此模式在舊版TVSDK中稱為自訂廣告標籤。 此模式會標籤已置入VOD資料流中之廣告的開始和結束時間。 當有型別的時間範圍標籤時 `MARK` 在串流中，初始位置為 `Mode.MARK` 產生者 `CustomMarkerOpportunityGenerator` 解決者 `CustomRangeResolver`. 未插入任何廣告。

* **DELETE** 對象 `DELETE` 時間範圍，初始 `placementInformation` 型別 `Mode.DELETE` 建立與解析者： `CustomRangeResolver`. `DeleteRangeTimelineOperation` 會定義要從時間軸移除的範圍，而TVSDK會使用 `removeByLocalTime` 從Adobe Video Engine (AVE) API完成此操作。 如果存在DELETE範圍和Adobe Primetime廣告決策中繼資料，則會先刪除範圍，然後 `AuditudeResolver` 使用典型的Adobe Primetime ad decisioning工作流程解析廣告。

* **REPLACE** 對象 `REPLACE` 時間範圍，兩個初始值 `placementInformations` 已建立，一個 `Mode.DELETE` 和一個 `Mode.REPLACE`. `CustomRangeResolver` 先刪除時間範圍，然後刪除 `AuditudeResolver` 插入指定的廣告 `replaceDuration` 放入時間軸中。 若否 `replaceDuration` 指定時，伺服器會決定要插入的內容。

為了支援這些自訂時間範圍作業，TVSDK提供下列功能：

* 多個內容解析器

   一個串流可以有多個根據廣告訊號模式和廣告中繼資料的內容解析器。 此行為會隨著廣告訊號模式和廣告中繼資料的不同組合而改變。
* 使用多個初始機會 `CustomMarkerOpportunityGenerator`.
* 新的廣告訊號模式， `CUSTOM_RANGES`.

   廣告會根據來自外部來源的時間範圍資料放置，例如JSON檔案。
