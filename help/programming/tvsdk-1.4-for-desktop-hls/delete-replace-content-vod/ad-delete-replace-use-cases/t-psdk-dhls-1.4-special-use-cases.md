---
title: 特殊用例
description: 特殊用例
copied-description: true
exl-id: 33aad8cc-5939-4890-bc89-32d6bbf1fa4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 特殊用例{#special-use-cases}

TVSDK支援自定義範圍設定，而不是標準廣告設定。 例如，如果定義了MARK範圍，則會忽略廣告的插入設定。 如果定義了REPLACE範圍，則TVSDK會自動使用 `CustomRanges` 信令模式。

1. `ReplaceRange` 無更換持續時間

   如果缺少更換持續時間，則實際更換持續時間由伺服器確定。 此中放置的廣告數 `AdBreak` 也由伺服器確定。

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. 具有替換持續時間的MARK和DELETE範圍

   額外的替換持續時間將被忽略。
