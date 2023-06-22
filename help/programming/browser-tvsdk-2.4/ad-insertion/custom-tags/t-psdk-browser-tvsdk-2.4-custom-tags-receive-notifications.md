---
description: 若要接收資訊清單中標籤的相關通知，請接聽AdobePSDK.TimedMetadataEvent。
title: 新增計時中繼資料通知的接聽程式
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 新增計時中繼資料通知的接聽程式{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的相關通知，請接聽AdobePSDK.TimedMetadataEvent。

新增時 `TimedMetadata` 物件建立後，MediaPlayer會傳送 `AdobePSDK.TimedMetadataEvent`.

1. 實作適當的接聽程式。

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. 註冊事件監聽器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3中繼資料會透過相同的傳送 `Events.TimedMetadataEvent`. 您可以使用 `timedMetadata.type` 屬性以區分TAG和ID3。
