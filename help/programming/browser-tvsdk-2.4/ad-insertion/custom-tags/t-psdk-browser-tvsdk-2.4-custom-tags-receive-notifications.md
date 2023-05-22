---
description: 要接收有關清單中標籤的通知，請偵聽AdobePSDK.TimedMetadataEvent。
title: 為定時元資料通知添加偵聽器
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 為定時元資料通知添加偵聽器{#add-listeners-for-timed-metadata-notifications}

要接收有關清單中標籤的通知，請偵聽AdobePSDK.TimedMetadataEvent。

新 `TimedMetadata` 建立對象，MediaPlayer調度 `AdobePSDK.TimedMetadataEvent`。

1. 實施適當的偵聽器。

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

ID3元資料通過同一 `Events.TimedMetadataEvent`。 您可以使用 `timedMetadata.type` 用於區分TAG和ID3的屬性。
