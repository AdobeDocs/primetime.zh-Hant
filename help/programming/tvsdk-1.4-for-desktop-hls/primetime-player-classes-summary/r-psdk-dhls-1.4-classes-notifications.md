---
description: 這些類描述有關錯誤、警告和某些活動的消息，這些事件是用於記錄和調試的。
title: 通知類
exl-id: d8af783f-1e80-4e50-89b8-97643ff6670b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 通知類 {#notification-classes}

這些類描述有關錯誤、警告和某些活動的消息，這些事件是用於記錄和調試的。

包： [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 類名 | 說明 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供資訊性消息、警告和錯誤的類。 封裝中單個通知事件的對象表示 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)。 |
| [通知代碼](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 返回與提供的通知代碼關聯的說明，並為通知對象提供數字常數。 |
| [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 儲存通知對象日誌的類。 循環清單 [通知歷史記錄項](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) 提供對通知事件歷史記錄清單的訪問的對象。 即，它維護一個元素清單，每個元素都包含 [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) 類。 |
| [通知歷史記錄項](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 在循環清單中定義條目的類 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) 並保存通知及其時間戳。 |
| [通知類型](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含支援的通知類型的類。 |
