---
description: 您可以將VOD內容中的時間間隔指定為廣告中斷。
title: 標籤範圍
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 標籤範圍{#mark-ranges}

您可以將VOD內容中的時間間隔指定為廣告中斷。

在這個例子中， `TimeRanges` 在 `begin` 和 `end` 在 `localTime` 將標籤為 `AdBreak` 在時間軸中。 忽略其他廣告設定。

>[!NOTE]
>
>如果您只想將內容中的某些範圍標籤為廣告（不插入動態廣告），請建立 `CustomRangeMetadata` ，並將類型指定為具有定義的自定義範圍的MARK操作。

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
