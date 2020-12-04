---
description: TVSDK支援程式化刪除和取代VOD串流中的廣告內容。
seo-description: TVSDK支援程式化刪除和取代VOD串流中的廣告內容。
seo-title: 自訂時間範圍作業
title: 自訂時間範圍作業
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# 自訂時間範圍作業{#custom-time-range-operations}

TVSDK支援程式化刪除和取代VOD串流中的廣告內容。

刪除和取代功能可延伸自訂廣告標籤功能。 自訂廣告標籤會將主要內容的區段標示為廣告相關內容句點。 除了標籤這些時間範圍外，您也可以刪除和取代時間範圍。

廣告刪除和取代是透過`TimeRange`元素實作，這些元素可識別VOD串流中不同類型的時間範圍：標籤、刪除和替換。 對於這些自訂時間範圍類型，您可以執行相應的作業，包括刪除和取代廣告內容。

對於廣告刪除和取代，TVSDK使用下列&#x200B;*自訂時間範圍作業*&#x200B;模式：

* **MARK**
（這些在舊版TVSDK中稱為自訂廣告標籤）。它們會標籤已置入VOD串流之廣告的開始和結束時間。 當串流中有MARK類型的時間範圍標籤時，初始放置 
`Mode.MARK` 由生成和解析 `CustomAdMarkersContentResolver`。不會插入廣告。

* **DELETEF**
或DELETE時間範圍，初始 
`placementInformation` 類型 `Mode.DELETE` 建立並由相應解析 `DeleteContentResolver`。`ContentRemoval` 是新的定 `timelineOperation` 義要從時間軸移除的範圍。TVSDK使用Adobe Video Engine(AVE)API的`removeByLocalTime`來協助該作業。 如果有DELETE範圍和Adobe Primetime廣告決策（先前稱為Auditude）中繼資料，則會先刪除範圍，然後`AuditudeResolver`會使用一般的Adobe Primetime廣告決策工作流程來解析廣告。

* ****
REPLACEF或REPLACE時間範圍，兩個初始 
`placementInformations` 一個 `Mode.DELETE` 和 `Mode.REPLACE`一個`DeleteContentResolver`會先刪除時間範圍，然後`AuditudeResolver`會將指定`replaceDuration`的廣告插入時間軸。 如果未指定`replaceDuration`，則伺服器將確定要插入的內容。

為支援這些自訂時間範圍作業，TVSDK提供下列功能：

* 多種內容解析器

   流可以基於廣告信令模式和廣告元資料具有多個內容解析器。 行為會隨著廣告信號模式和廣告中繼資料的不同組合而改變。
* 多個初始`PlacementInformations``DefaultMediaPlayer`根據要由`MediaPlayerClient`解析的廣告信令模式和廣告元資料建立初始`PlacementInformations`的清單。

* 新的廣告信令模式：自訂時間範圍

   廣告會根據來自外部來源（例如JSON檔案）的「時間範圍」資料來放置。