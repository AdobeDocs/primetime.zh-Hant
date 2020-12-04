---
description: 您可以將廣告插入VOD內容。
seo-description: 您可以將廣告插入VOD內容。
seo-title: 以廣告取代時間範圍
title: 以廣告取代時間範圍
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# 以ad{#replace-time-ranges-with-an-ad}取代時間範圍

您可以將廣告插入VOD內容。

在這種情況下，`localTime`中`begin`和`end`之間的`TimeRanges`會從時間軸中移除。 它們被`begin`的`AdBreak`替換為`begin+replaceDuration`。 如果取代持續時間不存在為參數，伺服器會在傳回的Adbreak上做出判斷。

>[!NOTE]
>
>您應始終為自訂範圍提供特定的取代持續時間。 如果沒有廣告要取代此自訂範圍，請提供0的取代持續時間。

以Primetime廣告決策廣告取代範圍。

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replacement-duration": 15000 
                },
                {
                    "begin": 69000,
                    "end": 99000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 251000,
                    "end": 281000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 514000,
                    "end": 544000,
                    "replacement-duration": 30000
                } ]
            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - Replace TimeRange with Auditude Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```

