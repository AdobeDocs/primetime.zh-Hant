---
title: 自訂VOD資產的範例
description: 自訂VOD資產的範例
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 自訂VOD資產的範例{#example-of-a-customized-vod-asset}

以下是自訂VOD資產的範例：

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

您的應用程式可設定下列情境：

* 發生以下情況時通知： `#EXT-X-ASSET` 標籤或您已訂閱的任何其他自訂標簽名稱集會存在於檔案中。
* 插入廣告的時機 `#EXT-X-AD` 標籤或任何其他自訂標簽名稱，可在資料流中找到。
