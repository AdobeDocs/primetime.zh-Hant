---
description: 您可以從時間軸移除localTime中開始和結束之間的TimeRanges。
title: 刪除範圍
exl-id: afa2f520-144f-47b4-b271-50c8e4d138d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 刪除範圍 {#delete-ranges}

您可以移除 `TimeRanges` 介於 `begin` 和 `end` 在 `localTime` 從時間軸。

>[!TIP]
>
>若只要移除內容中的特定範圍，請建立 `CustomRangeMetadata` 執行個體並指定型別為 `DELETE` 作業中定義的自訂範圍。

廣告對應必須如廣告伺服器所定義的那樣使用。

1. 若要刪除包含Adobe Primetime ad decisioning廣告的範圍：

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
                   "type": "delete",
                   "time-range-list": [
                       {
                           "begin": 0,
                           "end": 20000
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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```
