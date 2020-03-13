---
description: 若要接收資訊清單中標籤的通知，請監聽AdobePSDK.TimedMetadataEvent。
seo-description: 若要接收資訊清單中標籤的通知，請監聽AdobePSDK.TimedMetadataEvent。
seo-title: 新增計時中繼資料通知的監聽器
title: 新增計時中繼資料通知的監聽器
uuid: c82c5549-0ab6-4343-a766-5176e784d4cb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 新增計時中繼資料通知的監聽器{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的通知，請監聽AdobePSDK.TimedMetadataEvent。

建立新物 `TimedMetadata` 件時，MediaPlayer會進行派單 `AdobePSDK.TimedMetadataEvent`。

1. 實作適當的監聽器。

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. 註冊事件偵聽器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3中繼資料會透過相同的方式傳送 `Events.TimedMetadataEvent`。 您可以使用 `timedMetadata.type` 屬性來區分TAG和ID3。

