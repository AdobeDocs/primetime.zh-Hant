---
description: 您可以將廣告插入VOD內容。
title: 以廣告取代時間範圍
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 以廣告{#replace-time-ranges-with-an-ad}取代時間範圍

您可以將廣告插入VOD內容。

`localTime`中`begin`和`end`之間的`TimeRanges`會從時間軸中移除。 這些範圍由`begin`的`AdBreak`取代為`begin+replaceDuration`。 如果`replacement-duration`不存在作為參數，則伺服器對返回的`Adbreak`進行確定。

>[!TIP]
>
>您應始終為自訂範圍提供`replacement-duration`。 如果沒有廣告要取代此自訂範圍，請提供`replacement-duration`，共0個。

1. 若要以Primetime廣告決策廣告取代範圍：

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
           "metadata": {
               "time-ranges": {
                   "type": "replace",
                   "time-range-list": [
                       {
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
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```
