---
description: 可以從時間軸中刪除localTime中開始和結束之間的TimeRange。
title: 刪除範圍
exl-id: a91cd7ac-d60f-43bb-a783-ccc1b9b9e7fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 刪除範圍{#delete-ranges}

可以從時間軸中刪除localTime中開始和結束之間的TimeRange。

>[!TIP]
>
>要僅從內容中刪除某些範圍，請建立 `CustomRangeMetadata` 實例並將類型指定為 `DELETE` 定義的自定義範圍。

廣告映射必須按照廣告伺服器的定義使用。

1. 要刪除帶有Adobe Primetime廣告決策廣告的範圍，請執行以下操作：

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
