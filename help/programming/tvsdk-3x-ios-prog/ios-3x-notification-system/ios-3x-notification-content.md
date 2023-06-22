---
description: PTNotification物件提供有關播放器狀態變更、警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態的變更。
title: 通知內容
exl-id: 62423718-b154-4105-82b2-f6e389105ec8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 播放器狀態、活動、錯誤和記錄的通知 {#notifications-player-status-activity-errors-logging}

`PTNotification` 物件會提供有關播放器狀態變更、警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態的變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊，建立用於診斷和驗證的記錄系統。

>[!NOTE]
>
>TVSDK也使用 *`notification`* 參考 `NSNotifications` ( `PTMediaPlayer` 通知) *`event`* 通知，傳送以提供播放器活動的相關資訊。

TVSDK也有問題 `PTMediaPlayerNewNotificationItemEntryNotification` 問題發生時 `PTNotification`.

您可以實作事件接聽程式來擷取和回應事件。 許多事件提供 `PTNotification` 狀態通知。

## 通知內容 {#notification-content}

`PTNotification` 提供與播放器狀態相關的資訊。

TVSDK提供以下專案的時間順序清單： `PTNotification` 通知。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`：資訊、警告或錯誤。
   * `code`：通知的數字表示法。
   * `name`：可讀取的通知說明，例如SEEK_ERROR
   * `metadata`：包含通知相關資訊的索引鍵/值組。 例如，名為的金鑰 `URL` 提供一個值，該值為與通知相關的URL。

   * `innerNotification`：對另一個的參照 `PTNotification` 直接影響此通知的物件。

您可以將此資訊儲存在本機，供日後分析使用，或傳送至遠端伺服器以供記錄及圖形化顯示。

## 通知設定 {#notification-setup}

TVSDK會為基本通知設定播放器，但您必須為自訂通知完成相同的設定。

有兩個實作 `PTNotification`：

* 接聽
* 若要新增自訂通知至 `PTNotificationHistory`

若要收聽通知，TVSDK會將 `PTNotification` 類別並將其附加至 `PTMediaPlayerItem`，此專案會附加至PTMediaPlayer執行個體。 只有一個 `PTNotificationHistory` 執行個體依據 `PTMediaPlayer`.

>[!IMPORTANT]
>
>如果您要新增自訂，您的應用程式而不是TVSDK必須執行這些步驟。

## 聆聽通知 {#listen-to-notifications}

有兩種方式可監聽 `PTNotification` 中的通知 `PTMediaPlayer`：

1. 手動檢查 `PTNotificationHistory` 的 `PTMediaPlayerItem` 使用計時器並檢查差異：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用已張貼的 [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) 的 `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. 註冊至 `NSNotification` 透過使用的例項 `PTMediaPlayer` 您要從中取得通知的來源：

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 實作通知回呼 {#implement-notification-callbacks}

您可以實作通知回呼。

透過取得 `PTNotification` 從 `NSNotification` 使用者資訊和讀取其值，使用 `PTMediaPlayerNotificationKey`：

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## 新增自訂通知 {#add-custom-notifications}

新增自訂通知的方式：建立新的 `PTNotification` 並將其新增至 `PTNotificationHistory` 透過使用目前的 `PTMediaPlayerItem`：

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
