---
description: 這些類提供用於廣告、命名空間和跟蹤的元資料。
title: 元資料類
exl-id: 4014b496-7fc4-4fa9-98da-28350668d35f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 元資料類 {#metadata-classes}

這些類提供用於廣告、命名空間和跟蹤的元資料。

包： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| 名稱 | 說明 |
|---|---|
| [AdSigningMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | 枚舉類，用於在短語中顯示支援的信令模式。 |
| [音頻設定](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 擴展的類 `Metadata` 特別是短語。 提供要配置的屬性以解析給定媒體項的短語廣告。 必須設定所有必需的屬性，包括區域ID、媒體ID和廣告伺服器URL，才能配置播放器以成功解析廣告。 |
| [位元組陣列元資料](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | 已棄用。 使用 `Metadata`。 |
| [預設元資料鍵](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | 課。 |
| [元資料](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定義用於配置播放器和其他對象的所有可用元資料的通用介面。 |
| [元資料節點](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 已棄用。 使用 `Metadata`。 |
| [元資料實用程式](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | 處理元資料的方法類。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入到媒體流中的定時元資料的原始表示的類。 |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | 包含時間元資料（在播放清單或流中）支援的類型的類，如ID3元資料或標籤。 |
