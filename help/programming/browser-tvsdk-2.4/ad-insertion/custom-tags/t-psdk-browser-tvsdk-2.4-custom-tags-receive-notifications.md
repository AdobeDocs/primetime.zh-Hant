---
description: 若要接收資訊清單中標籤的通知，請監聽AdobePSDK.TimedMetadataEvent。
title: 新增計時中繼資料通知的監聽器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# 為計時中繼資料通知新增監聽器{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的通知，請監聽AdobePSDK.TimedMetadataEvent。

當建立新的`TimedMetadata`物件時，MediaPlayer會調度`AdobePSDK.TimedMetadataEvent`。

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

ID3中繼資料會透過相同的`Events.TimedMetadataEvent`傳送。 您可以使用`timedMetadata.type`屬性來區分TAG和ID3。

