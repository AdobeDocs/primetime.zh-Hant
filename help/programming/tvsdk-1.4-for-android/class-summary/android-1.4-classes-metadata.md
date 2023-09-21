---
description: 這些類別提供廣告、名稱空間和追蹤的中繼資料。
title: 中繼資料類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 中繼資料類別{#metadata-classes}

這些類別提供廣告、名稱空間和追蹤的中繼資料。

封裝： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 名稱 | 說明 |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 類別，提供解析指定媒體專案之廣告時應設定的屬性。 必須設定所有必要屬性，才能設定播放器以成功解析廣告。 |
| AuditudeMetadata | 已棄用。 使用AuditudeSettings。 |
| [Auditudesettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 擴充Java的類別 `AdvertisingMetadata` 特別針對片語。 提供針對指定媒體專案解析片語廣告要設定的屬性。 您必須設定所有必要的屬性（包括區域ID、媒體ID和廣告伺服器URL），以設定播放器以成功解析廣告。 |
| [中繼資料](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定義通用介面，用於設定播放器和其他物件所有可用的中繼資料。 |
| [中繼資料節點](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 用來儲存任意索引鍵值配對的泛型資料結構類別。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入媒體串流中的計時中繼資料原始表示法類別。 |
