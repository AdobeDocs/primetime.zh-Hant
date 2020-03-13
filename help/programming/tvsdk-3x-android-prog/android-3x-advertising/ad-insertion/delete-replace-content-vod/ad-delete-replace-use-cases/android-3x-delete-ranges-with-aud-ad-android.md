---
description: 您可以從時間軸移除localTime中開始和結束之間的TimeRange。
seo-description: 您可以從時間軸移除localTime中開始和結束之間的TimeRange。
seo-title: 刪除範圍
title: 刪除範圍
uuid: 2aaea7a0-5d52-49a1-901c-f71e4b081d91
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 刪除範圍 {#delete-ranges}

您可以從時 `TimeRanges` 間軸 `begin` 中移 `end` 除和移 `localTime` 除之間。

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
