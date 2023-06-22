---
description: 參考實作會說明如何設定廣告的播放器，包括為廣告插入設定視訊中繼資料，並將前段廣告、中段廣告和後段廣告解析為VOD或即時/線性視訊資料流。 它也會說明如何處理可點按的廣告。
title: 廣告插入
exl-id: 3c2d8fca-2a0e-4577-81f3-7b390f6396e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 廣告插入 {#ad-insertion}

參考實作會說明如何設定廣告的播放器，包括為廣告插入設定視訊中繼資料，並將前段廣告、中段廣告和後段廣告解析為VOD或即時/線性視訊資料流。 它也會說明如何處理可點按的廣告。

設定廣告插入播放器的程式包括：

* **輸入摘要：** 使用廣告中繼資料填入輸入摘要。 另請參閱 [目錄格式](../set-up-dev-environment/exploring-code/catalog-format.md).
* **參考實作摘要配接器：** 正在剖析輸入摘要以填入廣告中繼資料物件。
* **AdsManager：** 使用AdsManager擷取廣告中繼資料並建立對應的AdProvider。
