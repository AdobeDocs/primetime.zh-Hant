---
description: 您可以決定是隻解析在使用者目前即時點之後發生的廣告，還是同時解析在目前即時點之前發生的廣告。
title: 為DVR視窗載入廣告
exl-id: f0799002-5cba-41c2-86bb-9ccf6b906357
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 為DVR視窗載入廣告 {#load-ad-for-a-dvr-window}

您可以決定是隻解析在使用者目前即時點之後發生的廣告，還是同時解析在目前即時點之前發生的廣告。

當使用者在DVR資料流開始時開始檢視內容時，TVSDK會在該時間解析該資料流的所有廣告。 不過，當使用者開始檢視內容時，您可以決定是僅解析使用者目前即時點之後發生的廣告，還是解析目前即時點之前發生的廣告。

>[!TIP]
>
>在目前的即時點之後解決廣告的速度較快，但如果使用者向後搜尋，此選項會防止播放器播放先前出現的廣告。

## 控制DVR視窗的廣告載入 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

若要控制DVR視窗的廣告載入，請執行下列動作：

若要載入整個串流的所有廣告，請將 `PTAdMetadata.enableDVRAds` 屬性至 `YES`.

>[!NOTE]
>
>預設值為 `NO`，此選項只會從目前的即時點載入廣告。

例如：

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```
