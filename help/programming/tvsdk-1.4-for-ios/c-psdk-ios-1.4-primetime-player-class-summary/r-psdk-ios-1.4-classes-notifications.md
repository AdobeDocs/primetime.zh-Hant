---
description: 這些類別會說明TVSDK為了記錄與偵錯目的而發出的錯誤、警告和一些活動的相關訊息。
title: 通知類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 通知類別{#notification-classes}

這些類別會說明TVSDK為了記錄與偵錯目的而發出的錯誤、警告和一些活動的相關訊息。

| 類別名稱 | 說明 |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 描述導致播放器停止播放的錯誤通知類別。 這是 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) 的通知型別ERROR。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出Primetime播放器架構所傳送的所有通知。 |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供資訊性訊息、警告和錯誤的類別。 封裝單一通知事件的物件表示 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 儲存通知物件記錄的類別 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 提供通知事件歷史記錄清單存取權的物件。 也就是說，它會維護一個元素清單，每個元素都包含個別的 [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 定義中循環清單專案的類別 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 並保留通知及其時間戳記。 |
