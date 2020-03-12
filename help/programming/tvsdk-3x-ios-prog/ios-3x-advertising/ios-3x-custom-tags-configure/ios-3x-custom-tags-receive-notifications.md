---
description: 若要接收資訊清單中標籤的通知，請實作適當的通知接聽程式。
seo-description: 若要接收資訊清單中標籤的通知，請實作適當的通知接聽程式。
seo-title: 新增計時中繼資料通知的監聽器
title: 新增計時中繼資料通知的監聽器
uuid: b6939011-a6ff-4342-8e7c-3a0c805ee91c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 新增計時中繼資料通知的監聽器 {#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的通知，請實作適當的通知接聽程式。

您可以監聽下列事件來監控計時中繼資料，這些事件會通知您的應用程式相關活動：

* `PTTimedMetadataChangedNotification`:每次在剖析內容時識別唯一的訂閱標籤時，TVSDK會準備新物件並調 `PTTimedMetadata` 度此通知。

   物件包含您所訂閱之標籤的名稱、此標籤將出現的播放中的本機時間，以及其他資料。

* `PTMediaPlayerTimeChangeNotification` :對於資訊清單／播放清單定期重新整理的即時／線性串流，更新的播放清單／資訊清單中可能會顯示其他自訂標籤，因此 `TimedMetadata` 可能會將其他物件新增至屬 `MediaPlayerItem.timedMetadata` 性。

   發生此情況時，此事件會通知您的應用程式。

   以下列其中一種方式擷取計時中繼資料。

   * 將應用程式設定為將自身作為監聽器添加到通 `PTTimedMetadataChangedNotification` 知中，並使用獲取對象 `PTTimedMetadataKey`。

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * 訪問 `timedMetadataCollection` 的屬 `PTMediaPlayerItem`性，該屬性包含迄今 `PTTimedMetadata` 已通知的所有對象。