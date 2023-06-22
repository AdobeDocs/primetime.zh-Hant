---
description: 您可以將廣告插入VOD內容。
title: 以廣告取代時間範圍
exl-id: b341d337-e190-4e2d-bad6-579771bcc577
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 以廣告取代時間範圍{#replace-time-ranges-with-an-ad}

您可以將廣告插入VOD內容。

在這種情況下， `TimeRanges` 介於 `begin` 和 `end` 在 `localTime` 都會從時間軸移除。 這些區段會由 `AdBreak` 之 `begin` 至 `begin+replaceDuration`. 如果replacement-duration不是作為引數存在，則伺服器會判斷傳回的Adbreak。

>[!NOTE]
>
>您應該一律為自訂範圍提供特定的取代期間。 如果沒有意圖取代此自訂範圍的廣告，請提供取代持續時間0。

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
