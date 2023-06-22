---
description: TVSDK支援程式化地刪除和取代VOD串流中的廣告內容。
title: 自訂時間範圍作業
exl-id: 10aa3609-d5d0-49e2-959f-d72d8dbd6ef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 自訂時間範圍作業 {#custom-time-range-operations}

TVSDK支援程式化地刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為與廣告相關的內容句號。 除了標示這些時間範圍外，您也可以刪除和取代時間範圍。

使用實作廣告刪除和取代 `TimeRange` 可識別VOD資料流中不同型別時間範圍的元素：標籤、刪除和取代。 對於每種自訂時間範圍型別，您可以執行對應的操作，包括刪除和取代廣告內容。

對於廣告刪除和取代，TVSDK會使用下列專案 *自訂時間範圍作業* 模式：

* **標籤**
（在舊版TVSDK中，這些被稱為自訂廣告標籤）。 它們會標籤已置入VOD資料流中廣告的開始和結束時間。 當串流中有MARK型別的時間範圍標籤時，初始位置為 
`Mode.MARK` 由產生並解析 `CustomAdMarkersContentResolver`. 未插入任何廣告。

* **DELETE**
若為DELETE時間範圍，則為初始值 
`placementInformation` 型別 `Mode.DELETE` 由對應的建立和解析 `DeleteContentResolver`. `ContentRemoval` 是新的 `timelineOperation` 會定義要從時間軸移除的範圍。 TVSDK使用 `removeByLocalTime` 從Adobe Video Engine (AVE) API取得資料，以利該作業。 如果存在DELETE範圍和Adobe Primetime ad decisioning （先前稱為Auditude）中繼資料，則會先刪除範圍，然後 `AuditudeResolver` 使用一般Adobe Primetime ad decisioning工作流程解析廣告。

* **REPLACE**
對於REPLACE時間範圍，兩個初始值 
`placementInformations` 已建立，一個 `Mode.DELETE` 和一個 `Mode.REPLACE`. 此 `DeleteContentResolver` 先刪除時間範圍，然後刪除 `AuditudeResolver` 插入指定的廣告 `replaceDuration` 放入時間軸中。 若否 `replaceDuration` 指定時，伺服器會決定要插入的內容。

為了支援這些自訂時間範圍作業，TVSDK提供下列功能：

* 多個內容解析器

   一個串流可以有多個根據廣告訊號模式和廣告中繼資料的內容解析器。 此行為會隨著廣告訊號模式和廣告中繼資料的不同組合而改變。
* 多個初始 `PlacementInformations` 此 `DefaultMediaPlayer` 建立初始清單 `PlacementInformations` 根據將由解析的廣告訊號模式和廣告中繼資料 `MediaPlayerClient`.

* 新廣告訊號模式：自訂時間範圍

   廣告會根據來自外部來源的時間範圍資料放置（例如JSON檔案）。
