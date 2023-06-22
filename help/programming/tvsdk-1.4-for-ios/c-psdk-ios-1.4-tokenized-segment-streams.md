---
description: 透過內容傳遞網路(CDN)傳遞的HLS資料流有時可以使用資訊清單和區段請求上的驗證Token進行驗證。 這些權杖可以作為URL引數或Cookie標頭提供。
title: 代碼化區段資料流
exl-id: 20a3e8a2-2e9d-4c0d-abea-66edcbcf0003
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 代碼化區段資料流{#tokenized-segment-streams}

透過內容傳遞網路(CDN)傳遞的HLS資料流有時可以使用資訊清單和區段請求上的驗證Token進行驗證。 這些權杖可以作為URL引數或Cookie標頭提供。

主要資訊清單(m3u8)回應中以Cookie形式提供的Token不會與區段(ts)請求共用，即使區段請求是針對相同網域亦然。 若要在區段請求中啟用這些Cookie的分享，請在 `PTMetadata` 提供給播放器專案的例項： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在資料流開始播放之前，系統會先對主要資訊清單(m3u8)提出其他要求。

>[!IMPORTANT]
>
>只有執行iOS 8或以上版本的裝置才支援此Cookie共用功能。
