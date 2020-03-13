---
description: 您可以將VOD內容中的時間間隔指定為廣告插播。
seo-description: 您可以將VOD內容中的時間間隔指定為廣告插播。
seo-title: 標籤範圍
title: 標籤範圍
uuid: eb99a1c2-6c0c-40a4-bac2-98dce45acfad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 標籤範圍{#mark-ranges}

您可以將VOD內容中的時間間隔指定為廣告插播。

在此情況下， `TimeRanges` 在和 `begin` 中之間 `end` ，將 `localTime` 在時間軸中標 `AdBreak` 記為。 其他廣告設定會被忽略。

>[!NOTE]
>
>如果您只想將內容中的特定範圍標示為廣告（沒有動態廣告插入），請建立例項，並指定類型為具有已定義自訂範圍的MARK `CustomRangeMetadata` 作業。

1. 標籤範圍。

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "time-ranges": {
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
                       "begin": 0,
                       "end": 15000
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
                    } ]
               }
           }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```

