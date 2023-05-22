---
description: 您可以將廣告插入視頻點播內容。
title: 用廣告替換時間範圍
exl-id: b341d337-e190-4e2d-bad6-579771bcc577
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 用廣告替換時間範圍{#replace-time-ranges-with-an-ad}

您可以將廣告插入視頻點播內容。

在這個例子中， `TimeRanges` 在 `begin` 和 `end` 在 `localTime` 從時間軸中刪除。 替換為 `AdBreak` 共 `begin` 至 `begin+replaceDuration`。 如果replacement-duration不作為參數存在，伺服器將對返回的Adbreak進行確定。

>[!NOTE]
>
>您應始終為自定義範圍提供特定的替換持續時間。 如果沒有廣告要替換此自定義範圍，請提供替換持續時間0。

用黃金時段廣告決策廣告替換範圍。

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
