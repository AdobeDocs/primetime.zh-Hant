---
description: 'null'
seo-description: 'null'
seo-title: 特殊使用案例
title: 特殊使用案例
uuid: 066bc256-4fdf-4083-b23e-0a916b3b532f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 特殊使用案例{#special-use-cases}

TVSDK偏好自訂範圍設定，而非標準廣告設定。 例如，如果已定義MARK範圍，則會忽略廣告的插入設定。 如果已定義REPLACE範圍，TVSDK會自動使用信 `CustomRanges` 令模式。

1. `ReplaceRange` 無需更換持續時間

   如果缺少更換持續時間，則實際更換持續時間由伺服器確定。 此處放置的廣告數 `AdBreak` 量也由伺服器決定。

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

1. 使用替換持續時間標籤和刪除範圍

   額外的替換持續時間將被忽略。
