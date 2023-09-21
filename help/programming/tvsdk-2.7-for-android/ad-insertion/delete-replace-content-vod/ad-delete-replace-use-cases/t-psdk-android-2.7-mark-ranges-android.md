---
description: 您可以在VOD內容中將時間間隔指定為廣告插播。
title: 標籤範圍
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 標籤範圍 {#mark-ranges}

您可以在VOD內容中將時間間隔指定為廣告插播。

此 `TimeRanges` 介於 `begin` 和 `end` 在 `localTime` 將標示為 `AdBreak` 在時間軸中。 其他廣告設定則會被忽略。

>[!TIP]
>
>如果您只想將內容中的某些範圍標示為廣告，而不想插入動態廣告，請建立 `CustomRangeMetadata` 例項，並將型別指定為 `MARK` 作業中定義的自訂範圍。

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
