---
description: 您可以決定是只解析使用者目前即時點之後發生的廣告，還是也要解析目前即時點之前發生的廣告。
seo-description: 您可以決定是只解析使用者目前即時點之後發生的廣告，還是也要解析目前即時點之前發生的廣告。
seo-title: DVR視窗的載入廣告
title: DVR視窗的載入廣告
uuid: 3ae1fbf6-deae-4f39-a17d-43d1fe3cb975
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# DVR視窗的載入廣告 {#load-ad-for-a-dvr-window}

您可以決定是只解析使用者目前即時點之後發生的廣告，還是也要解析目前即時點之前發生的廣告。

當使用者在DVR串流開始檢視內容時，TVSDK會解析當時串流的所有廣告。 不過，當使用者在串流開始後的某個點開始檢視內容時，您可以決定是只解析使用者目前即時點之後發生的廣告，還是也要解析目前即時點之前發生的廣告。

>[!TIP]
>
>在目前即時點之後解析廣告的速度較快，但如果使用者向後搜尋，這個選項會防止播放器播放先前顯示的廣告。

## 控制DVR視窗的廣告載入 {#section_2D93E2E947644D66B6F6ED1DD6742C25}

若要控制DVR視窗的廣告載入：

    要載入整個流的所有廣告，請將「PTAdMetadata.enableDVRAds」屬性設定為「YES」。

>[!NOTE]
>
>預設值為， `NO`且此選項僅從目前即時點載入廣告。

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
