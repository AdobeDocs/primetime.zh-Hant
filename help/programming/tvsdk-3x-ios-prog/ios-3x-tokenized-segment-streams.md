---
description: 透過內容傳送網路(CDN)傳送的HLS串流，有時可在資訊清單和區段要求上使用驗證Token進行驗證。 這些Token可以做為URL參數或Cookie標題提供。
title: Token化區段串流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 已標籤的區段串流{#tokenized-segment-streams}

透過內容傳送網路(CDN)傳送的HLS串流，有時可在資訊清單和區段要求上使用驗證Token進行驗證。 這些Token可以做為URL參數或Cookie標題提供。

在主資訊清單(m3u8)回應上提供作為Cookie的Token，即使區段請求是針對相同網域，也不會與區段(ts)請求共用。 若要在區段請求中啟用這些Cookie的共用，請在提供給播放器項目的`PTMetadata`例項上設定下列屬性： 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

在串流開始播放之前，會向主資訊清單(m3u8)提出額外要求。

>[!IMPORTANT]
>
>只有執行iOS 8或以上版本的裝置才支援此Cookie共用功能。

