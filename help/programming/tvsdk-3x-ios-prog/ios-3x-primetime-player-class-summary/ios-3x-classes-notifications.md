---
description: 這些類別會說明TVSDK為了記錄及偵錯目的而發出之錯誤、警告和一些活動的相關訊息。
title: 通知類別
exl-id: 97a01418-f747-4a6e-bfa5-e680438e40c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 通知類別 {#notification-classes}

這些類別會說明TVSDK為了記錄及偵錯目的而發出之錯誤、警告和一些活動的相關訊息。

| **類別名稱** | **說明** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 說明導致播放器停止播放的錯誤通知類別。 這是 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) 通知型別ERROR的。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出Primetime播放器架構傳送的所有通知。 |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供資訊性訊息、警告和錯誤的類別。 封裝中單一通知事件的物件表示 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 儲存通知物件記錄的類別 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 提供通知事件歷史記錄清單存取權的物件。 也就是說，它會維護一個元素清單，每個元素都包含 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 定義中循環清單專案的類別 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 和會儲存通知及其時間戳記。 |
