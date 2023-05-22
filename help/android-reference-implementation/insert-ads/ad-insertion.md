---
description: 該參考實現說明了如何為廣告設定播放器，包括設定用於廣告插入的視頻元資料並將預卷、中卷和後卷廣告解析成VOD或即時/線性視頻流。 它還說明了如何處理可點擊的廣告。
title: 廣告插入
exl-id: 3c2d8fca-2a0e-4577-81f3-7b390f6396e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 廣告插入 {#ad-insertion}

該參考實現說明了如何為廣告設定播放器，包括設定用於廣告插入的視頻元資料並將預卷、中卷和後卷廣告解析成VOD或即時/線性視頻流。 它還說明了如何處理可點擊的廣告。

設定廣告插入播放器的過程包括：

* **輸入源：** 用廣告元資料填充輸入源。 請參閱 [目錄格式](../set-up-dev-environment/exploring-code/catalog-format.md)。
* **參考實現源適配器：** 分析輸入源以填充廣告元資料對象。
* **AdsManager:** 使用AdsManager檢索廣告元資料並建立相應的AdProvider。
