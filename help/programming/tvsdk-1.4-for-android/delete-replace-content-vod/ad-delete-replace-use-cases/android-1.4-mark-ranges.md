---
description: 您可以在VOD內容中將時間間隔指定為廣告插播。
title: 標籤範圍
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 標籤範圍{#mark-ranges}

您可以在VOD內容中將時間間隔指定為廣告插播。

在這種情況下， `TimeRanges` 介於 `begin` 和 `end` 在 `localTime` 將標示為 `AdBreak` 在時間軸中。 其他廣告設定會被忽略。

>[!NOTE]
>
>如果您只想將內容中的某些範圍標示為廣告（沒有動態廣告插入），請建立 `CustomRangeMetadata` 執行個體，並將型別指定為具有已定義自訂範圍的MARK作業。

1. 標示範圍。

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
