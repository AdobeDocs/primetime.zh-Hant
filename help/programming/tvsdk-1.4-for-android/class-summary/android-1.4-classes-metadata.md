---
description: 這些類提供用於廣告、命名空間和跟蹤的元資料。
title: 元資料類
exl-id: 3d98c5e1-6792-419b-9638-f156f1eafd1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 元資料類{#metadata-classes}

這些類提供用於廣告、命名空間和跟蹤的元資料。

包： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 名稱 | 說明 |
|---|---|
| [廣告元資料](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 提供應配置用於解析給定媒體項的廣告的屬性的類。 必須設定所有必需的屬性才能配置播放器以成功解析廣告。 |
| 審核元資料 | 已棄用。 使用AuditudeSettings。 |
| [音頻設定](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 擴展Java的類 `AdvertisingMetadata` 特別是短語。 提供要配置的屬性以解析給定媒體項的短語廣告。 必須設定所有必需的屬性，包括區域ID、媒體ID和廣告伺服器URL，才能配置播放器以成功解析廣告。 |
| [元資料](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定義用於配置播放器和其他對象的所有可用元資料的通用介面。 |
| [元資料節點](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 用於儲存任意鍵值對的類型資料結構類。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒體流中的定時元資料的原始表示的類。 |
