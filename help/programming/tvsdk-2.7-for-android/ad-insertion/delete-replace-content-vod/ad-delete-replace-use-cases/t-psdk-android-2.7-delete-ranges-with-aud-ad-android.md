---
description: 您可以從時間軸移除localTime中開始和結束之間的TimeRange。
seo-description: 您可以從時間軸移除localTime中開始和結束之間的TimeRange。
seo-title: 刪除範圍
title: 刪除範圍
uuid: 637829a7-efa8-4b83-9a04-ef01c043621f
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 刪除範圍{#delete-ranges}

您可以從時間軸移除localTime中開始和結束之間的TimeRange。

>[!TIP]
>
>若要僅從內容移除特定範圍，請建立例 `CustomRangeMetadata` 項並指定類型為使用已定義 `DELETE` 自訂範圍的作業。

廣告地圖必須依廣告伺服器的定義使用。

1. 若要使用Adobe Primetime廣告決策廣告刪除範圍：

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

