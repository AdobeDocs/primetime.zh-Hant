---
description: 通過內容分發網路(CDN)傳送的HLS流有時可以使用清單和段請求上的驗證令牌進行驗證。 這些令牌可以作為URL參數或cookie標頭提供。
title: 標籤化段流
exl-id: c7b441a7-63b6-4930-93a1-12ef6b72474e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 標籤化段流 {#tokenized-segment-streams}

通過內容分發網路(CDN)傳送的HLS流有時可以使用清單和段請求上的驗證令牌進行驗證。 這些令牌可以作為URL參數或cookie標頭提供。

在主清單(m3u8)響應上作為cookie提供的令牌不與段(ts)請求共用，即使段請求是針對同一域。 要在段請求中啟用這些Cookie的共用，請在 `PTMetadata` 提供給播放器項的實例： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在流開始播放之前對主清單(m3u8)發出附加請求。

>[!IMPORTANT]
>
>此Cookie共用功能僅在運行iOS8或更高版本的設備上受支援。
