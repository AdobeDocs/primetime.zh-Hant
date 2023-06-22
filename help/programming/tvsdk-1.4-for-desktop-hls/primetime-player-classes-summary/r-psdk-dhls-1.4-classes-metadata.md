---
description: 這些類別提供廣告、名稱空間和追蹤的中繼資料。
title: 中繼資料類別
exl-id: 4014b496-7fc4-4fa9-98da-28350668d35f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 中繼資料類別 {#metadata-classes}

這些類別提供廣告、名稱空間和追蹤的中繼資料。

封裝： [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| 名稱 | 說明 |
|---|---|
| [AdSignalingMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | 列舉類別會公開片語中支援的訊號模式。 |
| [Auditudesettings](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | 擴充的類別 `Metadata` 專門針對片語。 提供為解析指定媒體專案的片語廣告而要設定的屬性。 您必須設定所有必要的屬性（包括區域ID、媒體ID和廣告伺服器URL），才能設定播放器以成功解析廣告。 |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | 已棄用。 使用 `Metadata`. |
| [DefaultMetadataKey](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | 類別。 |
| [中繼資料](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | 定義通用介面，用於設定播放器和其他物件所有可用的中繼資料。 |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | 已棄用。 使用 `Metadata`. |
| [MetadataUtils](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | 使用中繼資料的方法類別。 |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | 插入媒體串流中計時中繼資料的原始表示類別。 |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | 包含定時中繼資料（在播放清單或串流中）之支援型別（例如ID3中繼資料或標籤）的類別。 |
