---
seo-title: 自訂廣告標籤的JSON物件
title: 自訂廣告標籤的JSON物件
uuid: 2c05d9ce-a22f-4829-bfea-9dcf0dc7cd6d
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 自訂廣告標籤{#json-object-for-custom-ad-markers}的JSON物件

當類型為自訂廣告標籤時，下方的程式碼區塊會定義「詳細資料」JSON物件。

IFeedItemAdapter:getStreamMetadata()返回的MetadataNode包含2個條目：
1. 鍵類型為`com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY`的條目，以及由`TimeRangeCollection.toMetadata()`返回的元資料節點實例的值。
1. 第二條目具有類型`com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED`的鍵，其值如下的&#x200B;*adjust-seek-position*&#x200B;屬性。

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
| 調整尋道位置 | true或false，用來設定中繼資料節點中com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED索引鍵的值。 |
| 時間範圍 | JSON物件陣列，指示每個廣告標籤的時間範圍。 每個JSON物件項目會對應至com.adobe.mediacore.utils.TimeRange的例項。 |
| time-ranges.begin | 以毫秒錶示的值，用於指示廣告標籤的開始時間。 |
| time-ranges.end | 以毫秒錶示的值，用於指示廣告標籤的結束時間。 |

請參閱TVSDK檔案，以取得自訂廣告標籤如何運作的詳細資訊。
