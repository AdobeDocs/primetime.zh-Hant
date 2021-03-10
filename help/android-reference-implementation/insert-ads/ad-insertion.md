---
description: 參考實作說明如何設定廣告的播放器，包括設定廣告插入的視訊中繼資料，以及將前、中、後段廣告解析為VOD或即時／線性視訊串流。 它也說明如何處理可點選廣告。
title: 廣告插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 廣告插入{#ad-insertion}

參考實作說明如何設定廣告的播放器，包括設定廣告插入的視訊中繼資料，以及將前、中、後段廣告解析為VOD或即時／線性視訊串流。 它也說明如何處理可點選廣告。

設定廣告插入播放器的程式包括：

* **輸入動態消息：** 以廣告中繼資料填入輸入動態消息。請參閱[目錄格式](../set-up-dev-environment/exploring-code/catalog-format.md)。
* **參考實作摘要適配器：** 剖析輸入摘要以填入廣告中繼資料物件。
* **AdsManager：使** 用AdsManager擷取廣告中繼資料並建立對應的AdProvider。