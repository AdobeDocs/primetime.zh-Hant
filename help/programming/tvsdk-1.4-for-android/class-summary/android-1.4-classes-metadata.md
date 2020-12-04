---
description: 這些類別提供廣告、命名空間和追蹤的中繼資料。
seo-description: 這些類別提供廣告、命名空間和追蹤的中繼資料。
seo-title: 中繼資料類別
title: 中繼資料類別
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# 中繼資料類別{#metadata-classes}

這些類別提供廣告、命名空間和追蹤的中繼資料。

套件：[com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| 名稱 | 說明 |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | 提供屬性的類別，該屬性應設定為解析特定媒體項目的廣告。 必須設定所有必要屬性，才能設定播放器，以成功解析廣告。 |
| AuditudeMetadata | 已過時。 使用AuditudeSettings。 |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 專門用於擴展Phrase的Java `AdvertisingMetadata`的類。 提供要配置的屬性，用於解析給定媒體項目的短語廣告。 您必須設定所有必要屬性，包括區域ID、媒體ID和廣告伺服器URL，才能設定播放器以成功解析廣告。 |
| [中繼資料](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定義一般介面，以針對您的播放器和其他物件設定所有可用的中繼資料。 |
| [中繼資料節點](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 用於儲存任意鍵值對的類似資料結構的類。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 用於插入媒體流中的定時元資料的原始表示的類。 |