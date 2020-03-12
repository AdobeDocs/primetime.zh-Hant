---
description: 您可以將廣告插入VOD內容。
seo-description: 您可以將廣告插入VOD內容。
seo-title: 以廣告取代時間範圍
title: 以廣告取代時間範圍
uuid: 8f09560c-bca3-4662-bc58-6c9cd0892476
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 以廣告取代時間範圍 {#replace-time-ranges-with-an-ad}

您可以將廣告插入VOD內容。

從時 `TimeRanges` 間軸 `begin` 中移 `end` 除和 `localTime` 中之間的。 這些範圍會由 `AdBreak` 到 `begin` 取 `begin+replaceDuration`代。 如果 `replacement-duration` 不存在作為參數，則伺服器會對返回的參數進行確定 `Adbreak`。

>[!TIP]
>
>您應一律提供自 `replacement-duration` 訂範圍。 如果沒有廣告要取代此自訂範圍，請提供0 `replacement-duration` 個廣告。

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

