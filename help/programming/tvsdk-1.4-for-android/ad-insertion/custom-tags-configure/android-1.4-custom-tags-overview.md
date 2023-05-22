---
title: 自定義VOD資產示例
description: 自定義VOD資產示例
copied-description: true
exl-id: 62b3ddf2-4c00-4402-8178-85143736b15f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 自定義VOD資產示例{#example-of-a-customized-vod-asset}

下面是自定義VOD資產的示例：

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

您的應用程式可以設定以下方案：

* 在 `#EXT-X-ASSET` 標籤或您訂閱的任何其他自定義標籤名稱集都存在於檔案中。
* 在 `#EXT-X-AD` 在流中找到標籤或任何其他自定義標籤名稱。
