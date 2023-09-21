---
description: 參考實施說明如何設定廣告的播放器，包括設定廣告插入的視訊中繼資料，並將前段、中段和後段廣告解析為VOD或即時/線性視訊資料流。 它也會說明如何處理可點按的廣告。
title: 廣告插入
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 廣告插入 {#ad-insertion}

參考實施說明如何設定廣告的播放器，包括設定廣告插入的視訊中繼資料，並將前段、中段和後段廣告解析為VOD或即時/線性視訊資料流。 它也會說明如何處理可點按的廣告。

設定廣告插入播放器的程式包括：

* **輸入摘要：** 以廣告中繼資料填入輸入摘要。 另請參閱 [目錄格式](../set-up-dev-environment/exploring-code/catalog-format.md).
* **參考實作摘要配接器：** 剖析輸入摘要以填入廣告中繼資料物件。
* **AdsManager：** 使用AdsManager擷取廣告中繼資料，並建立對應的AdProvider。
