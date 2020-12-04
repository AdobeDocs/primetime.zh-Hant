---
description: 這些類別說明錯誤、警告和某些活動的訊息，這些訊息是出於記錄和除錯的目的。
seo-description: 這些類別說明錯誤、警告和某些活動的訊息，這些訊息是出於記錄和除錯的目的。
seo-title: 通知類
title: 通知類
uuid: 3befc64b-4abd-47df-9c45-215b49029757
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# 通知類{#notification-classes}

這些類別說明錯誤、警告和某些活動的訊息，這些訊息是出於記錄和除錯的目的。

套件：[com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 類別名稱 | 說明 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供資訊性消息、警告和錯誤的類。 封裝[NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)中單一通知事件的對象表示。 |
| [通知代碼](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 返回與提供的通知代碼關聯的說明，並為通知對象提供數字常數。 |
| [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 儲存通知對象日誌的類。 [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html)物件的圓形清單，可讓您存取通知事件歷史記錄清單。 也就是說，它維護一個元素清單，每個元素包含[Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html)類的單獨實例。 |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 在[NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)中定義循環清單中條目並保存通知及其時間戳的類。 |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含支援通知類型的類別。 |

