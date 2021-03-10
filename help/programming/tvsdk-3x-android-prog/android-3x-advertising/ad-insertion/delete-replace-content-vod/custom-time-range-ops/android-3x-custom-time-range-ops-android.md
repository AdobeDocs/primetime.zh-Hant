---
description: CustomRangeMetadata類別可識別VOD串流標籤、刪除和取代中不同類型的時間範圍。 對於這些自訂時間範圍類型，您可以執行相應的作業，包括刪除和取代廣告內容。
title: 自訂時間範圍作業
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# 自訂時間範圍作業{#custom-time-range-operations}

CustomRangeMetadata類別可識別VOD串流中不同類型的時間範圍：標籤、刪除和替換。 對於這些自訂時間範圍類型，您可以執行相應的作業，包括刪除和取代廣告內容。

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

對於廣告刪除和取代，TVSDK使用下列&#x200B;*自訂時間範圍作業*&#x200B;模式：

* **** MARKThis模式在舊版TVSDK中稱為自訂廣告標籤。此模式會標示已置入VOD串流之廣告的開始和結束時間。 當流中存在類型`MARK`的時間範圍標籤時，由`CustomMarkerOpportunityGenerator`生成`Mode.MARK`的初始位置，並由`CustomRangeResolver`解析。 不會插入廣告。

* **** DELETEF或 `DELETE` 時間範圍時，會 `placementInformation` 由創 `Mode.DELETE` 建和解析初始類型 `CustomRangeResolver`。`DeleteRangeTimelineOperation` 定義要從時間軸移除的範圍，而TVSDK會 `removeByLocalTime` 使用Adobe視訊引擎(AVE)API來完成此作業。如果有DELETE範圍和Adobe Primetime廣告決策中繼資料，則會先刪除範圍，然後`AuditudeResolver`會使用典型的Adobe Primetime廣告決策工作流程來解析廣告。

* **REPLACEEF** 或 `REPLACE` 時間範圍，會建立兩 `placementInformations` 個初始值，一 `Mode.DELETE` 個 `Mode.REPLACE`。`CustomRangeResolver` 先刪除時間範圍，然後將指 `AuditudeResolver` 定的廣告插入 `replaceDuration` 時間軸。如果未指定`replaceDuration`，則伺服器將確定要插入的內容。

為支援這些自訂時間範圍作業，TVSDK提供下列功能：

* 多種內容解析器

   流可以基於廣告信令模式和廣告元資料具有多個內容解析器。 行為會隨著廣告信號模式和廣告中繼資料的不同組合而改變。
* 使用`CustomMarkerOpportunityGenerator`的多個初始機會。
* 新的廣告信令模式`CUSTOM_RANGES`。

   廣告會根據來自外部來源（例如JSON檔案）的「時間範圍」資料來放置。