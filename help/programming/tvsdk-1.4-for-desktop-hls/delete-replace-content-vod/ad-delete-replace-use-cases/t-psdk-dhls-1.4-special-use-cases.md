---
title: 特殊使用案例
description: 特殊使用案例
copied-description: true
exl-id: 33aad8cc-5939-4890-bc89-32d6bbf1fa4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 特殊使用案例{#special-use-cases}

TVSDK偏好自訂範圍設定，而非標準廣告設定。 例如，如果已定義MARK範圍，則會忽略廣告的插入設定。 如果已定義REPLACE範圍，TVSDK會自動使用 `CustomRanges` 訊號模式。

1. `ReplaceRange` 無替代期間

   如果缺少取代期間，實際的取代期間由伺服器決定。 置入此的廣告數量 `AdBreak` 也由伺服器決定。

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

1. 以取代持續時間標籤和DELETE範圍

   會忽略額外的取代期間。
