---
description: 您可以從時間軸移除localTime中開始和結束之間的TimeRanges。
title: 刪除範圍
exl-id: 1c0f7718-8a40-4fc8-b70b-f751d8ff40a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 0%

---

# 刪除範圍{#delete-ranges}

您可以從時間軸移除localTime中開始和結束之間的TimeRanges。

>[!NOTE]
>
>如果您只想從內容中移除某些範圍，且必須使用廣告對應由廣告伺服器定義，請建立 `CustomRangeMetadata` 例項，並將型別指定為具有已定義自訂範圍的DELETE作業。

刪除包含Adobe Primetime ad decisioning廣告的範圍。

```
{   
    "properties": [],
    "stream": {
        "manifests": [
            {
                "url": "https://xyz.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                "type": "hls"
            }
        ],
     
        "metadata": {
            "time-ranges": {
                "type": "delete",
                "time-range-list": [
                    {
                        "begin": 0,
                        "end": 20000
                    },
                    {
                        "begin": 69000,
                        "end": 99000
                    },
                    {
                        "begin": 251000,
                        "end": 281000
                    },
                    {
                        "begin": 514000,
                        "end": 544000
                    }
                ]
     
            },
            "ad": {
                "targeting": [
                    {
                        "value": "MulAdsAvail12346",
                        "key": "osmfKeyMulAdsAvail12346"
                    }
                ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - DELETE TimeRange with Primetime ad decisioning Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```
