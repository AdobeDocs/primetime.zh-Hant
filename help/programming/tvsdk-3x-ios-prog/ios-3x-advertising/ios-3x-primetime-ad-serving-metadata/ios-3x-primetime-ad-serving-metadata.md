---
description: TVSDK支援VOD和即時/線性資料流的解析和插入廣告。
title: Primetime廣告伺服器中繼資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 概觀 {#primetime-ad-server-metadata-overview}

TVSDK支援VOD和即時/線性資料流的解析和插入廣告。

## 先決條件

在視訊內容中加入廣告之前，請提供下列中繼資料資訊：

* A `mediaID`，可識別要播放的特定內容。
* 您的 `zoneID`，可識別您的公司或網站。
* 您的廣告伺服器網域，這會指定您指派的廣告伺服器的網域。
* 其他目標定位引數。

## 設定Primetime廣告伺服器中繼資料 {#section_86C4A3B2DF124770B9B7FD2511394313}

您的應用程式必須向TVSDK提供所需的 `PTAuditudeMetadata` 連線至廣告伺服器的資訊。

若要設定廣告伺服器中繼資料：

1. 建立例項 [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) 並設定其屬性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 設定 `PTAuditudeMetadata` 執行個體作為目前的中繼資料 `PTMediaPlayerItem` 使用建立中繼資料 `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   範例如下：

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```
