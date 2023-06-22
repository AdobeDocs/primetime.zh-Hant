---
title: 直接廣告插播的JSON物件
description: 當型別值為直接廣告插播時，詳細說明JSON物件
exl-id: d5e3ddd5-b963-4e7d-b04b-087d4fe96faf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 直接廣告插播的JSON物件{#json-object-for-direct-ad-breaks}

當型別值是直接廣告插播時，下列程式碼區塊會定義詳細資訊JSON物件。

此 `MetadataNode` 傳回者 `IFeedItemAdapter:getStreamMetadata()` 包含具有型別索引鍵的專案 `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 和字串值，代表以下的詳細資料JSON物件值。

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
| `tag` | 對應至中標籤欄位的字串 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | 表示廣告插播的開始時間，對應至中的時間欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`. 值0表示前段廣告。 |
| `replace` | 表示廣告插播取代持續時間，對應至 `replaceDuration` 中的欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | 在指定的廣告插播期間要播放的廣告清單，將對應至 `List<Ad>` 中的欄位 `com.adobe.mediacore.timeline.advertising.AdBreak`. |

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
| `url` | 廣告內容的URL，對應至中的url欄位 `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | 廣告持續時間，對應至中的持續時間欄位 `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | 說明字串。 |
