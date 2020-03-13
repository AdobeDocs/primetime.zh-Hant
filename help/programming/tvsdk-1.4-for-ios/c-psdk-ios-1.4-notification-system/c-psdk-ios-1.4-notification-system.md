---
description: PTNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
seo-description: PTNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
seo-title: 播放器狀態、活動、錯誤和記錄的通知
title: 播放器狀態、活動、錯誤和記錄的通知
uuid: 59716a66-3736-4076-8011-8104bfe3a83a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 播放器狀態、活動、錯誤和記錄的通知 {#notifications-for-player-status-activity-errors-and-logs-overview}

PTNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊建立診斷和驗證的記錄系統。

>[!IMPORTANT]
>
>TVSDK也會使 *`notification`* 用（通知） `NSNotifications` 通 `PTMediaPlayer`*`event`* 知來提供播放器活動的相關資訊。

TVSDK也會在發 `PTMediaPlayerNewNotificationItemEntryNotification` 生問題時發 `PTNotification`生。

您實作事件監聽器以擷取並回應事件。 許多事件都會提 `PTNotification` 供狀態通知。

## 通知內容 {#notification-content}

PTNotification提供與播放器狀態相關的資訊。

TVSDK提供通知的時間 `PTNotification` 清單。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，例如SEEK_ERROR
   * `metadata`:包含通知相關資訊的金鑰／值配對。 例如，名為的索引鍵 `URL` 提供與通知相關的URL值。

   * `innerNotification`:對其他對象的 `PTNotification` 引用直接影響此通知。

您可以將這些資訊儲存在本機以供日後分析，或將它傳送至遠端伺服器以進行記錄和圖形表示。

## 通知設定 {#notification-setup}

TVSDK會針對基本通知設定播放器，不過您必須完成自訂通知的相同設定。

有兩種實施 `PTNotification`:

* 要收聽
* 若要新增自訂通知至 `PTNotificationHistory`

若要監聽通知，TVSDK會執 `PTNotification` 行個體化類別並將其附加至 `PTMediaPlayerItem`PTMediaPlayer例項的例項。 每個例項 `PTNotificationHistory` 只有一 `PTMediaPlayer`個

>[!IMPORTANT]
>
>如果您要新增自訂，您的應用程式（而非TVSDK）必須執行這些步驟。

## 監聽通知 {#listen-to-notifications}

在中監聽通知有 `PTNotification` 兩種方式 `PTMediaPlayer`:

1. 使用計時器 `PTNotificationHistory` 手動檢 `PTMediaPlayerItem` 查的，並檢查差異：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用張貼 [的](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) NSNotification `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`。
1. 使用您 `NSNotification` 要收到通知的 `PTMediaPlayer` 例項，註冊至：

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 實作通知回呼 {#implement-notification-callbacks}

您可以實作通知回呼。

1. 從使用者資訊取得通知回呼， `PTNotification` 並使用 `NSNotification` 下列項目讀取其值，以實作通知回呼 `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## 新增自訂通知 {#add-custom-notifications}

若要新增自訂通知：建立新 `PTNotification` 的檔案，並 `PTNotificationHistory` 使用目前 `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
