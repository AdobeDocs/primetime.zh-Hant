---
description: 這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。
seo-description: 這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。
seo-title: 通知類
title: 通知類
uuid: 08c29efe-245d-4a6d-80c6-cd561cbf3b5f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# 通知類{#notification-classes}

這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。

| 類別名稱 | 說明 |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 說明導致播放器停止播放之錯誤通知的類別。 這是通知類型為ERROR的[PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出Primetime Player架構傳送的所有通知。 |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供資訊性消息、警告和錯誤的類。 封裝[PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)中單一通知事件的物件表示。 |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 儲存通知對象[PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html)對象日誌的類，該類提供對通知事件歷史記錄清單的訪問。 也就是說，它維護一個元素清單，每個元素包含一個單獨的[PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)實例 |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 在[PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)的循環清單中定義條目並保存通知及其時間戳的類。 |

