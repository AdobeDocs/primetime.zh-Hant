---
description: PTNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
title: 播放器狀態、活動、錯誤和記錄的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# 播放器狀態、活動、錯誤和記錄的通知{#notifications-for-player-status-activity-errors-and-logs-overview}

PTNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊建立診斷和驗證的記錄系統。

>[!IMPORTANT]
>
>TVSDK也使用&#x200B;*`notification`*&#x200B;來參考`NSNotifications`（`PTMediaPlayer`通知）*`event`*&#x200B;通知，以提供播放器活動的相關資訊。

TVSDK在發問`PTNotification`時也會發問`PTMediaPlayerNewNotificationItemEntryNotification`。

您實作事件監聽器以擷取並回應事件。 許多事件都提供`PTNotification`狀態通知。

## 通知內容{#notification-content}

PTNotification提供與播放器狀態相關的資訊。

TVSDK提供`PTNotification`通知的時間清單。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，例如SEEK_ERROR
   * `metadata`:包含通知相關資訊的金鑰／值配對。例如，名為`URL`的索引鍵提供與通知相關的URL值。

   * `innerNotification`:直接影響此通 `PTNotification` 知的對其它對象的引用。

您可以將這些資訊儲存在本機以供日後分析，或將它傳送至遠端伺服器以進行記錄和圖形表示。

## 通知設定{#notification-setup}

TVSDK會針對基本通知設定播放器，不過您必須完成自訂通知的相同設定。

`PTNotification`有兩種實現：

* 要收聽
* 若要新增自訂通知至`PTNotificationHistory`

若要監聽通知，TVSDK會執行個體化`PTNotification`類別，並將它附加至附加至PTMediaPlayer例項的`PTMediaPlayerItem`例項。 每個`PTMediaPlayer`只有一個`PTNotificationHistory`實例。

>[!IMPORTANT]
>
>如果您要新增自訂，您的應用程式（而非TVSDK）必須執行這些步驟。

## 監聽通知{#listen-to-notifications}

監聽`PTMediaPlayer`中`PTNotification`通知有兩種方式：

1. 使用計時器手動檢查`PTMediaPlayerItem`的`PTNotificationHistory`並檢查差異：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用`PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`的已發佈[NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html)。
1. 使用您想要收到通知的`PTMediaPlayer`例項，註冊至`NSNotification`:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 實施通知回呼{#implement-notification-callbacks}

您可以實作通知回呼。

1. 從`NSNotification`使用者資訊取得`PTNotification`並使用`PTMediaPlayerNotificationKey`讀取其值，以實作通知回呼：

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## 新增自訂通知{#add-custom-notifications}

若要新增自訂通知：
建立新的`PTNotification`，並使用目前的`PTMediaPlayerItem`將其新增至`PTNotificationHistory`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
