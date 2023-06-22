---
title: 自訂廣告標籤的JSON物件
description: 自訂廣告標籤的JSON物件
copied-description: true
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 自訂廣告標籤的JSON物件 {#json-object-for-custom-ad-markers}

當型別為自訂廣告標籤時，下方的程式碼區塊會定義「詳細資料」JSON物件。

IFeedItemAdapter：getStreamMetadata()傳回的MetadataNode包含2個專案：
1. 具有型別索引鍵的專案 `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 和傳回之MetadataNode例項的值 `TimeRangeCollection.toMetadata()`.
1. 第二個專案具有型別索引鍵 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` ，其值為 *adjust-seek-position* 屬性下方。

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| 屬性 | 說明 |
|---|---|
| adjust-seek-position | true或false，用來設定MetadataNode中索引鍵com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED的值。 |
| 時間範圍 | JSON物件的陣列，指出每個廣告標籤的時間範圍。 每個JSON物件專案都會對應至com.adobe.mediacore.utils.TimeRange的例項。 |
| time-ranges.begin | 表示廣告標籤開始時間的值（毫秒）。 |
| time-ranges.end | 表示廣告標籤結束時間的值（毫秒）。 |

請參閱TVSDK檔案，深入瞭解自訂廣告標籤如何運作。
