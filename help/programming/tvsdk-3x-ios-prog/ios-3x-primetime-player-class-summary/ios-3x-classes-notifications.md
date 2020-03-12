---
description: 這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。
seo-description: 這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。
seo-title: 通知類
title: 通知類
uuid: 8a276056-775f-432d-a4b4-722f6e4e278f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 通知類 {#notification-classes}

這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。

| **類別名稱** | **說明** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 說明導致播放器停止播放之錯誤通知的類別。 這是通知 [類型](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) ERROR的PTNotification。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出Primetime Player架構傳送的所有通知。 |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供資訊性消息、警告和錯誤的類。 封裝 [PTNotificationHistory中單一通知事件的物件表示](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)。 |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 儲存通知物件記錄 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 物件的類別，可存取通知事件記錄清單。 也就是說，它會維護元素清單，每個元素都包含 [PTNotification的個別例項](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 在 [PTNotificationHistory中定義循環清單中項的類](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) ，並保存通知及其時間戳。 |

