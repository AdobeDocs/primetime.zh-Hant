---
description: 若要接收資訊清單中標籤的相關通知，請實作適當的通知監聽器。
title: 為定時中繼資料通知新增接聽程式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 為定時中繼資料通知新增接聽程式 {#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的相關通知，請實作適當的通知監聽器。

您可以監聽下列事件來監視定時中繼資料，這些事件會通知您的應用程式相關活動：

* `PTTimedMetadataChangedNotification`：每次在剖析內容期間識別不重複訂閱標籤時，TVSDK都會準備新的 `PTTimedMetadata` 物件並傳送此通知。

  物件包含您訂閱的標簽名稱、此標籤出現所在的播放本地時間以及其他資料。

* `PTMediaPlayerTimeChangeNotification` ：針對資訊清單/播放清單定期重新整理的即時/線性資料流，更新的播放清單/資訊清單中可能會顯示其他自訂標籤，因此也會顯示其他自訂標籤 `TimedMetadata` 物件可新增至 `MediaPlayerItem.timedMetadata` 屬性。

  此事件會在發生時通知您的應用程式。

  以下列其中一種方式擷取計時中繼資料。

   * 設定您的應用程式，將其本身新增為監聽器 `PTTimedMetadataChangedNotification` 通知並擷取物件，使用 `PTTimedMetadataKey`.

     ```
     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
       name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
     
     - (void) onTimedMetadataChanged:(NSNotification *) notification { 
         NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
         PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
     }
     ```

   * 存取 `timedMetadataCollection` 屬性 `PTMediaPlayerItem`，包含所有 `PTTimedMetadata` 目前為止已收到通知的物件。
