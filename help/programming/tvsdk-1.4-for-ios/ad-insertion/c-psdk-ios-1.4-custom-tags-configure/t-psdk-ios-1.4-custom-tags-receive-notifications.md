---
description: 要接收有關清單中標籤的通知，請實現相應的通知偵聽器。
title: 為定時元資料通知添加偵聽器
exl-id: 259af856-797b-4a50-9add-f72132831ba1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 為定時元資料通知添加偵聽器 {#add-listeners-for-timed-metadata-notifications}

要接收有關清單中標籤的通知，請實現相應的通知偵聽器。

您可以通過偵聽以下事件來監視定時元資料，這些事件會通知您的應用程式相關活動：

* `PTTimedMetadataChangedNotification`:每次在分析內容期間標識唯一的預訂標籤時，TVSDK準備新的 `PTTimedMetadata` 對象並調度此通知。

   對象包含您訂閱的標籤的名稱、此標籤將出現的回放中的本地時間以及其他資料。

* `PTMediaPlayerTimeChangeNotification` :對於清單/播放清單定期刷新的即時/線性流，更新的播放清單/清單中可能會出現附加的自定義標籤，因此附加的 `TimedMetadata` 對象可能已添加到 `MediaPlayerItem.timedMetadata` 屬性。

   發生此情況時，此事件會通知您的應用程式。

   以下方法之一檢索定時元資料。

   * 將應用程式設定為將自身作為監聽器添加到 `PTTimedMetadataChangedNotification` 通知和讀取對象 `PTTimedMetadataKey`。

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * 訪問 `timedMetadataCollection` 物業 `PTMediaPlayerItem`，由 `PTTimedMetadata` 已通知的對象。
