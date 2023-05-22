---
description: TVSDK支援VOD流中廣告內容的寫程式刪除和替換。
title: 自定義時間範圍操作
exl-id: 10aa3609-d5d0-49e2-959f-d72d8dbd6ef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 自定義時間範圍操作 {#custom-time-range-operations}

TVSDK支援VOD流中廣告內容的寫程式刪除和替換。

刪除和替換特徵擴展了自定義和標籤特徵。 自定義廣告標籤將主內容的節標籤為與廣告相關的內容句點。 除了標籤這些時間範圍外，還可以刪除和替換時間範圍。

廣告刪除和替換通過 `TimeRange` 標識VOD流中不同類型時間範圍的元素：標籤、刪除和替換。 對於這些自定義時間範圍類型中的每種類型，可以執行相應的操作，包括刪除和替換廣告內容。

對於廣告刪除和替換，TVSDK使用以下 *自定義時間範圍操作* 模式：

* **標籤**
（這些標籤在TVSDK的早期版本中稱為自定義廣告標籤）。 它們標籤已放入VOD流的廣告的開始和結束時間。 當流中存在MARK類型的時間範圍標籤時，初始放置 
`Mode.MARK` 由 `CustomAdMarkersContentResolver`。 未插入廣告。

* **DELETE**
對於DELETE時間範圍，初始 
`placementInformation` 類型 `Mode.DELETE` 由相應的 `DeleteContentResolver`。 `ContentRemoval` 是新的 `timelineOperation` 定義要從時間軸中刪除的範圍。 TVSDK使用 `removeByLocalTime` 從Adobe視頻引擎(AVE)API中，以便於該操作。 如果存在DELETE範圍和Adobe Primetime和決策（以前稱為Auditude）元資料，則首先刪除該範圍，然後 `AuditudeResolver` 使用常規的Adobe Primetime廣告決策工作流解析廣告。

* **替換**
對於REPLACE時間範圍，兩個初始 
`placementInformations` 建立，一個 `Mode.DELETE` 一個 `Mode.REPLACE`。 的 `DeleteContentResolver` 先刪除時間範圍，然後刪除 `AuditudeResolver` 插入指定廣告 `replaceDuration` 進入時間軸。 否 `replaceDuration` 指定時，伺服器將確定插入的內容。

為支援這些自定義時間範圍操作，TVSDK提供了以下功能：

* 多個內容解析器

   流可以基於廣告信令模式和廣告元資料具有多個內容解析器。 行為隨著廣告信令模式和廣告元資料的不同組合而改變。
* 多個初始 `PlacementInformations` 的 `DefaultMediaPlayer` 建立初始清單 `PlacementInformations` 基於廣告信令方式和廣告元資料 `MediaPlayerClient`。

* 新廣告信令模式：自定義時間範圍

   廣告是基於來自外部源（如JSON檔案）的時間範圍資料進行放置的。
