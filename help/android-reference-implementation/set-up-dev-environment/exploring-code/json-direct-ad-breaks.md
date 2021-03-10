---
title: 直接廣告插播的JSON物件
description: 當類型值為直接廣告分段時，詳細資訊JSON物件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 直接廣告插播的JSON物件{#json-object-for-direct-ad-breaks}

下列程式碼區塊會定義當類型值為直接廣告插播時的詳細資料JSON物件。

`IFeedItemAdapter:getStreamMetadata()`傳回的`MetadataNode`包含鍵類型為`com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY`的項目，以及下方詳細資訊JSON物件值的字串表示法值。

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
| `tag` | 映射至`com.adobe.mediacore.timeline.advertising.AdBreak`中標籤欄位的字串。 |
| `time` | 指出廣告分段的開始時間，對應至`com.adobe.mediacore.timeline.advertising.AdBreak`中的時間欄位。 值0表示前段廣告。 |
| `replace` | 指出廣告分段取代持續時間，對應至`com.adobe.mediacore.timeline.advertising.AdBreak`的`replaceDuration`欄位。 |
| `ad-list` | 要在指定廣告分段期間播放的廣告清單，對應至`com.adobe.mediacore.timeline.advertising.AdBreak`中的`List<Ad>`欄位。 |

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
| `url` | 廣告內容的URL，會對應至`com.adobe.mediacore.timeline.advertising.Ad`中的url欄位。 |
| `duration` | 廣告的持續時間，對應至`com.adobe.mediacore.timeline.advertising.Ad`中的持續時間欄位。 |
| `tag` | 描述字串。 |

