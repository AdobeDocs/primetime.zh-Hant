---
description: TVSDK支援解析和插入用於視頻點播和即時/線性流的廣告。
title: 黃金時段廣告伺服器元資料
exl-id: f27657ac-4037-45e5-a658-ad9a783dd990
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支援解析和插入用於視頻點播和即時/線性流的廣告。

## 先決條件

在視頻內容中包括廣告之前，請提供以下元資料資訊：

* A `mediaID`，它標識要播放的特定內容。
* 您 `zoneID`，它標識您的公司或網站。
* 您的廣告伺服器域，它指定您分配的廣告伺服器的域。
* 其他目標參數。

## 設定Mogfire廣告伺服器元資料 {#section_86C4A3B2DF124770B9B7FD2511394313}

您的應用程式必須向TVSDK提供所需 `PTAuditudeMetadata` 連接到ad伺服器的資訊。

設定廣告伺服器元資料：

1. 建立實例 [PTAuditude元資料](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) 並設定其屬性。

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. 設定 `PTAuditudeMetadata` 實例作為當前的元資料 `PTMediaPlayerItem` 元資料 `PTAdResolvingMetadataKey`。

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   下面是一個示例：

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
