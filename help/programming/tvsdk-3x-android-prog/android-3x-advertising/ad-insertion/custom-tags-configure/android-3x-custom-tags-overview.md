---
title: 自訂VOD資產範例
description: 自訂VOD資產範例
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

您的應用程式可以設定下列案例：

* 當`#EXT-X-ASSET`標籤或您已訂閱的任何其他自訂標籤名稱集存在檔案時，會出現通知。
* 在串流中找到`#EXT-X-AD`標籤或任何其他自訂標籤名稱時插入廣告。

