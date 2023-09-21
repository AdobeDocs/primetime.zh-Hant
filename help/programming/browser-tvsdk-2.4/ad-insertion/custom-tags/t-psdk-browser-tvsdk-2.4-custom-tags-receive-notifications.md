---
description: 若要接收資訊清單中標籤的相關通知，請接聽AdobePSDK.TimedMetadataEvent。
title: 新增計時中繼資料通知的接聽程式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 新增計時中繼資料通知的接聽程式{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的相關通知，請接聽AdobePSDK.TimedMetadataEvent。

當新的 `TimedMetadata` 物件已建立，MediaPlayer會傳送 `AdobePSDK.TimedMetadataEvent`.

1. 實作適當的接聽程式。

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. 註冊事件接聽程式。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3中繼資料會透過相同的傳送 `Events.TimedMetadataEvent`. 您可以使用 `timedMetadata.type` 屬性以區分TAG和ID3。
