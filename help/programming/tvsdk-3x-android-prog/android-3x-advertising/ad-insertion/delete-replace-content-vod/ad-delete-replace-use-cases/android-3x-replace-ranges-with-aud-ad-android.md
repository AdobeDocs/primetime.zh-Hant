---
description: 您可以將廣告插入視頻點播內容。
title: 用廣告替換時間範圍
exl-id: bee5308a-f867-4824-84a8-751746785971
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 用廣告替換時間範圍 {#replace-time-ranges-with-an-ad}

您可以將廣告插入視頻點播內容。

的 `TimeRanges` 在 `begin` 和 `end` 在 `localTime` 從時間軸中刪除。 這些範圍由 `AdBreak` 共 `begin` 至 `begin+replaceDuration`。 如果 `replacement-duration` 不作為參數存在，伺服器將對返回的 `Adbreak`。

>[!TIP]
>
>您應始終提供 `replacement-duration` 的子菜單。 如果沒有廣告意在替換此自定義範圍，請提供 `replacement-duration` 0。

1. 要用黃金時段廣告決策替換這些範圍，請：

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
