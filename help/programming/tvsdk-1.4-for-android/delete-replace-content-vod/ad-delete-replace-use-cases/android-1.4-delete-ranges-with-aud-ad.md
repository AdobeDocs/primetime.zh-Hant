---
description: 您可以從時間軸移除localTime中開始和結束之間的TimeRange。
seo-description: 您可以從時間軸移除localTime中開始和結束之間的TimeRange。
seo-title: 刪除範圍
title: 刪除範圍
uuid: 2f4afa0d-69e3-4929-8dbd-b553c8a64d96
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 刪除範圍{#delete-ranges}

您可以從時間軸移除localTime中開始和結束之間的TimeRange。

>[!NOTE]
>
>如果您只想從內容移除特定範圍，而且廣告地圖必須如廣告伺服器所定義般使用，請建立例項，並指定類型為具有已定義自訂範圍的 `CustomRangeMetadata` DELETE作業。

使用Adobe Primetime廣告決策廣告刪除範圍。

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

