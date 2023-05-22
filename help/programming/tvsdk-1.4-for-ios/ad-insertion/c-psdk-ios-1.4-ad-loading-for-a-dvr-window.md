---
description: 您可以決定是僅解決用戶當前即時點之後出現的廣告，還是解決當前即時點之前的廣告。
title: 載入DVR窗口的廣告
exl-id: f0799002-5cba-41c2-86bb-9ccf6b906357
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 載入DVR窗口的廣告 {#load-ad-for-a-dvr-window}

您可以決定是僅解決用戶當前即時點之後出現的廣告，還是解決當前即時點之前的廣告。

當用戶開始在DVR流的開始處查看內容時，TVSDK解析當時該流的所有廣告。 但是，當用戶開始在流開始後的某個點查看內容時，您可以決定是僅解析在用戶當前即時點之後出現的廣告，還是也解析在當前即時點之前出現的廣告。

>[!TIP]
>
>在當前即時點之後解析廣告的速度更快，但如果用戶向後看，此選項會阻止玩家播放早前出現的廣告。

## DVR窗口的控制和載入 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

要控制DVR窗口的載入和載入，請執行以下操作：

要載入整個流的所有廣告，請設定 `PTAdMetadata.enableDVRAds` 屬性 `YES`。

>[!NOTE]
>
>預設值為 `NO`，並且此選項僅從當前即時點載入廣告。

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
