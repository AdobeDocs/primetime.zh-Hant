---
description: PTNotification對象提供有關播放器狀態、警告和錯誤更改的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。
title: 通知內容
exl-id: 62423718-b154-4105-82b2-f6e389105ec8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 播放器狀態、活動、錯誤和記錄的通知 {#notifications-player-status-activity-errors-logging}

`PTNotification` 對象提供有關播放器狀態、警告和錯誤更改的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。

您的應用程式可以檢索通知和狀態資訊。 您還可以使用通知資訊建立診斷和驗證的日誌記錄系統。

>[!NOTE]
>
>TVSDK還使用 *`notification`* 參考 `NSNotifications` ( `PTMediaPlayer` 通知) *`event`* 通知，被派送以提供有關播放器活動的資訊。

TVSDK也有問題 `PTMediaPlayerNewNotificationItemEntryNotification` 當 `PTNotification`。

實現事件偵聽器以捕獲和響應事件。 許多事件提供 `PTNotification` 狀態通知。

## 通知內容 {#notification-content}

`PTNotification` 提供與播放器狀態相關的資訊。

TVSDK提供按時間順序排列的 `PTNotification` 通知。 每個通知都包含以下資訊：

* 時間戳
* 包含以下元素的診斷元資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，如SEEK_ERROR
   * `metadata`:包含有關通知的相關資訊的鍵/值對。 例如，名為 `URL` 提供與通知相關的URL的值。

   * `innerNotification`:對另一個的引用 `PTNotification` 直接影響此通知的對象。

您可以將此資訊本地儲存以供以後分析，或將其發送到遠程伺服器以進行日誌記錄和圖形表示。

## 通知設定 {#notification-setup}

TVSDK為基本通知設定播放器，但必須完成自定義通知的相同設定。

有兩種實現 `PTNotification`:

* 聽
* 將自定義通知添加到 `PTNotificationHistory`

要收聽通知，TVSDK將 `PTNotification` 類並將其附加到實例 `PTMediaPlayerItem`，它附加到PTMediaPlayer實例。 只有一個 `PTNotificationHistory` 實例 `PTMediaPlayer`。

>[!IMPORTANT]
>
>如果要添加自定義項，則必須執行這些步驟。

## 偵聽通知 {#listen-to-notifications}

有兩種方法可以傾聽 `PTNotification` 通知 `PTMediaPlayer`:

1. 手動檢查 `PTNotificationHistory` 的 `PTMediaPlayerItem` 和計時器一起，並檢查其差異：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用已過帳 [NSN通知](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) 的 `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`。
1. 註冊到 `NSNotification` 使用 `PTMediaPlayer` 要從中獲取通知：

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 實現通知回調 {#implement-notification-callbacks}

您可以實施通知回叫。

通過獲取 `PTNotification` 從 `NSNotification` 使用 `PTMediaPlayerNotificationKey`:

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## 添加自定義通知 {#add-custom-notifications}

要添加自定義通知：新建 `PTNotification` 並加到 `PTNotificationHistory` 使用當前 `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
