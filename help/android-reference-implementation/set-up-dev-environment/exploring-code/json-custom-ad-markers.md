---
title: 自定義廣告標籤的JSON對象
description: 自定義廣告標籤的JSON對象
copied-description: true
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 自定義廣告標籤的JSON對象 {#json-object-for-custom-ad-markers}

當類型為自定義和標籤時，下面的代碼塊定義「詳細資訊」JSON對象。

IFeedItemAdapter:getStreamMetadata()返回的MetadataNode包含2個條目：
1. 鍵類型的條目 `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 和返回的MetadataNode實例的值 `TimeRangeCollection.toMetadata()`。
1. 第二個條目具有類型的鍵 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 值 *調整尋道位置* 屬性。

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
| 調整尋道位置 | true或false，用於在MetadataNode中設定com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED鍵的值。 |
| 時間範圍 | JSON對象陣列，指示每個廣告標籤的時間範圍。 每個JSON對象項都映射到com.adobe.mediacore.utils.TimeRange的實例。 |
| time-ranges.begin | 以毫秒錶示的廣告標籤的開始時間的值。 |
| time-ranges.end | 以毫秒錶示的廣告標籤結束時間的值。 |

有關自定義廣告標籤如何工作的詳細資訊，請參閱TVSDK文檔。
