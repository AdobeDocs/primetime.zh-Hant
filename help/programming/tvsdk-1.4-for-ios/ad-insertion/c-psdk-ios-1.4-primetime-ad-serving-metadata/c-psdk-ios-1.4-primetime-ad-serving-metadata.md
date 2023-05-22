---
description: TVSDK支援解析和插入用於視頻點播和即時/線性流的廣告。
title: 黃金時段廣告伺服器元資料
exl-id: 3723dd2f-292c-4ce5-9670-fda1b1f2b5df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 概述 {#primetime-ad-server-metadata-overview}

TVSDK支援解析和插入用於視頻點播和即時/線性流的廣告。

>[!NOTE]
>
>在視頻內容中包括廣告之前，請提供以下元資料資訊：
>
>* A `mediaID`，它標識要播放的特定內容。
>* 您 `zoneID`，它標識您的公司或網站。
>* 您的廣告伺服器域，它指定您分配的廣告伺服器的域。
>* 其他目標參數。
>


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

## 在全事件重播中啟用廣告 {#section_6016E1DAF03645C8A8388D03C6AB7571}

全事件重播(FER)是一種VOD資產，充當即時/DVR資產，因此您的應用程式必須採取步驟以確保廣告被正確放置。

對於即時內容，TVSDK使用清單中的元資料/提示來確定廣告的放置位置。 但是，有時即時/線性內容可能與VOD內容類似。 例如，當即時內容完成時， `EXT-X-ENDLIST` 標籤將附加到即時清單。 對於HLS, `EXT-X-ENDLIST` 標籤表示流是VOD流。 TVSDK無法自動將此流與正常的VOD流區分，以正確插入廣告。

您的應用程式必須通過指定以下內容來告訴TVSDK內容是即時還是視頻點播 `PTAdSignalingMode`。

對於FER流，Adobe Primetime廣告決定伺服器不應提供在開始播放之前需要在時間線上插入廣告中斷的清單。 這是視頻點播內容的典型過程。 相反，通過指定不同的信令模式，TVSDK從FER清單讀取所有提示點並進入廣告伺服器以請求廣告中斷。 此過程類似於即時/DVR內容。

除了與提示點相關聯的每個請求之外，TVSDK還對預卷廣告進行附加的廣告請求。

1. 從外部源（如vCMS）獲取應使用的信令模式。
1. 建立與廣告相關的元資料。
1. 如果必須覆蓋預設行為，請指定 `PTAdSignalingMode` 使用 `PTAdMetadata.signalingMode`。

   有效值為 `PTAdSignalingModeDefault`。 `PTAdSignalingModeManifestCues`, `PTAdSignalingModeServerMap`。

   在調用前必須設定廣告信令模式 `prepareToPlay`。 在TVSDK開始解析廣告並將其置於時間線上後，將忽略對廣告信令模式的更改。 為資源建立廣告元資料時設定模式。

1. 繼續播放。

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```
