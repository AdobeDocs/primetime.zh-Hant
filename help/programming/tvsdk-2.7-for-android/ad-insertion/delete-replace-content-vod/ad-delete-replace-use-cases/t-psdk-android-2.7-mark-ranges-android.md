---
description: 您可以將VOD內容中的時間間隔指定為廣告插播。
seo-description: 您可以將VOD內容中的時間間隔指定為廣告插播。
seo-title: 標籤範圍
title: 標籤範圍
uuid: 6ae2adee-fb7a-4cef-a8e8-ecf671ed3660
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 標籤範圍 {#mark-ranges}

您可以將VOD內容中的時間間隔指定為廣告插播。

介 `TimeRanges` 於和 `begin` 之間的 `end` 將 `localTime` 在時間軸中標 `AdBreak` 記為。 其他廣告設定會被忽略。

>[!TIP]
>
>如果您只想將內容中的特定範圍標示為廣告，而無動態廣告插入，請建立例項 `CustomRangeMetadata` ，並指定類型為已定義自訂 `MARK` 範圍的作業。

1. 標籤範圍：

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
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
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
                       }
                    ]
   
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

