---
seo-title: 直接廣告插播的JSON物件
title: 直接廣告插播的JSON物件
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: 當類型值為直接廣告分段時，詳細資訊JSON物件
seo-description: 當類型值為直接廣告分段時，詳細資訊JSON物件
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 直接廣告插播的JSON物件{#json-object-for-direct-ad-breaks}

下列程式碼區塊會定義當類型值為直接廣告插播時的詳細資料JSON物件。

傳回 `MetadataNode` 的項目 `IFeedItemAdapter:getStreamMetadata()` 包含以下詳細資訊JSON物件值的字串 `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 表示法類型和值的索引鍵。

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
| `time` | 指出廣告分段的開始時間，對應至中的時間欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`。 值0表示前段廣告。 |
| `replace` | 指出廣告分段取代持續時間，對應至中 `replaceDuration` 的欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |
| `ad-list` | 在指定廣告插播期間要播放的廣告清單，對應至中的 `List<Ad>` 欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |

下列程式碼區塊會定義廣告清單陣列的JSON物件。

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
| `url` | 廣告內容的URL，對應至中的URL欄位 `com.adobe.mediacore.timeline.advertising.Ad`。 |
| `duration` | 廣告的持續時間，對應至中的持續時間欄位 `com.adobe.mediacore.timeline.advertising.Ad`。 |
| `tag` | 描述字串。 |

