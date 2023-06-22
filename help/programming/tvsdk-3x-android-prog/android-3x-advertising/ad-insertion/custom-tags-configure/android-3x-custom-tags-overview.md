---
title: 自訂VOD資產範例
description: 自訂VOD資產範例
copied-description: true
exl-id: 4990ef96-f8bf-4b3b-83a0-979bf8c0e70c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 自訂VOD資產範例{#example-of-a-customized-vod-asset}

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

* 通知時間 `#EXT-X-ASSET` 標籤或您已訂閱的任何其他自訂標簽名稱集都存在於檔案中。
* 插入廣告的時機 `#EXT-X-AD` 標籤或任何其他自訂標籤名稱可在資料流中找到。
