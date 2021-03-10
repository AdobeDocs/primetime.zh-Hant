---
description: TVSDK支援解析和插入VOD和即時／線性串流的廣告。
title: Primetime廣告伺服器中繼資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 概述{#primetime-ad-server-metadata-overview}

TVSDK支援解析和插入VOD和即時／線性串流的廣告。

## 先決條件

在視訊內容中加入廣告之前，請提供下列中繼資料資訊：

* `mediaID`，可識別要播放的特定內容。
* 您的`zoneID`，可識別您的公司或網站。
* 您的廣告伺服器網域，指定您指派的廣告伺服器的網域。
* 其他定位參數。

## 設定Primetime廣告伺服器中繼資料{#section_86C4A3B2DF124770B9B7FD2511394313}

您的應用程式必須提供TVSDK必要的`PTAuditudeMetadata`資訊，才能連線至廣告伺服器。

若要設定廣告伺服器中繼資料：

1. 建立[PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html)實例並設定其屬性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 使用`PTAdResolvingMetadataKey`將`PTAuditudeMetadata`實例設定為當前`PTMediaPlayerItem`元資料的元資料。

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   以下是範例：

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
