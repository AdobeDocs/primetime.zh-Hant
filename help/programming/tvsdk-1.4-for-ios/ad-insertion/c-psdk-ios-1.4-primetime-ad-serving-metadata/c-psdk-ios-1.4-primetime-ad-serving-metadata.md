---
description: TVSDK支援解析和插入VOD和即時／線性串流的廣告。
title: Primetime廣告伺服器中繼資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# 概述{#primetime-ad-server-metadata-overview}

TVSDK支援解析和插入VOD和即時／線性串流的廣告。

>[!NOTE]
>
>在視訊內容中加入廣告之前，請提供下列中繼資料資訊：
>
>* `mediaID`，可識別要播放的特定內容。
>* 您的`zoneID`，可識別您的公司或網站。
>* 您的廣告伺服器網域，指定您指派的廣告伺服器的網域。
>* 其他定位參數。

>



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

## 在全事件重播中啟用廣告{#section_6016E1DAF03645C8A8388D03C6AB7571}

完整事件重播(FER)是VOD資產，可當成即時/DVR資產，因此您的應用程式必須採取步驟，以確保正確放置廣告。

對於即時內容，TVSDK會使用資訊清單中的中繼資料／提示來決定放置廣告的位置。 不過，有時即時／線性內容可能與VOD內容相似。 例如，當即時內容完成時，即時資訊清單會附加`EXT-X-ENDLIST`標籤。 對於HLS,`EXT-X-ENDLIST`標籤表示流是VOD流。 TVSDK無法自動區分此串流與一般VOD串流，以正確插入廣告。

您的應用程式必須透過指定`PTAdSignalingMode`來告知TVSDK內容是即時還是VOD。

對於FER串流，Adobe Primetime廣告決策伺服器不應提供在開始播放之前必須先插入時間軸的廣告插播清單。 這是VOD內容的典型程式。 相反地，TVSDK透過指定不同的信令模式，從FER資訊清單讀取所有提示點，並前往廣告伺服器，以請求廣告中斷。 此程式類似於即時/DVR內容。

除了與提示點相關的每個要求外，TVSDK還會針對前段廣告提出額外的廣告要求。

1. 從外部源（如vCMS）獲取應使用的信令模式。
1. 建立廣告相關的中繼資料。
1. 如果必須覆寫預設行為，請使用`PTAdMetadata.signalingMode`指定`PTAdSignalingMode`。

   有效值為`PTAdSignalingModeDefault`、`PTAdSignalingModeManifestCues`和`PTAdSignalingModeServerMap`。

   您必須在呼叫`prepareToPlay`之前設定廣告信令模式。 在TVSDK開始解析廣告並將其置於時間軸上後，會忽略對廣告訊號模式的變更。 為資源建立廣告中繼資料時，請設定模式。

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

