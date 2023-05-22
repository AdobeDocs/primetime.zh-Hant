---
title: 用於直接廣告分段的JSON對象
description: 當類型值為直接分段時，詳細說明JSON對象
exl-id: d5e3ddd5-b963-4e7d-b04b-087d4fe96faf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 用於直接廣告分段的JSON對象{#json-object-for-direct-ad-breaks}

當類型值為直接分段時，以下代碼塊定義詳細資訊JSON對象。

的 `MetadataNode` 返回 `IFeedItemAdapter:getStreamMetadata()` 包含鍵類型的條目 `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 以及下面詳細資訊JSON對象值的字串表示形式的值。

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| 屬性 | 說明 |
|---|---|
| `tag` | 映射到中的標籤欄位的字串 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |
| `time` | 指示廣告分段的開始時間，映射到中的時間欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`。 值0表示預滾廣告。 |
| `replace` | 指示廣告分段替換持續時間，映射到 `replaceDuration` 欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |
| `ad-list` | 在指定廣告分段期間要播放的廣告清單，映射到 `List<Ad>` 欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |

以下代碼塊定義ads-list陣列的JSON對象。

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| 屬性 | 說明 |
|---|---|
| `url` | 廣告內容的URL，映射到中的URL欄位 `com.adobe.mediacore.timeline.advertising.Ad`。 |
| `duration` | 廣告的持續時間，映射到中的持續時間欄位 `com.adobe.mediacore.timeline.advertising.Ad`。 |
| `tag` | 描述字串。 |
