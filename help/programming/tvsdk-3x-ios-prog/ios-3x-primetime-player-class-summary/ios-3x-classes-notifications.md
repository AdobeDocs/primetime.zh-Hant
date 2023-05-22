---
description: 這些類描述有關錯誤、警告和TVSDK為記錄和調試而發出的某些活動的消息。
title: 通知類
exl-id: 97a01418-f747-4a6e-bfa5-e680438e40c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 通知類 {#notification-classes}

這些類描述有關錯誤、警告和TVSDK為記錄和調試而發出的某些活動的消息。

| **類名** | **說明** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 描述導致播放器停止播放的錯誤通知的類。 這是 [PTN認證](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) 通知類型ERROR。 |
| [PTMediaPlayer通知](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出Mogine Player框架發送的所有通知。 |
| [PTN認證](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供資訊性消息、警告和錯誤的類。 封裝中單個通知事件的對象表示 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)。 |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 儲存通知對象日誌的類 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 提供對通知事件歷史記錄清單的訪問的對象。 即，它維護一個元素清單，每個元素都包含 [PTN認證](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 在循環清單中定義條目的類 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 並保存通知及其時間戳。 |
