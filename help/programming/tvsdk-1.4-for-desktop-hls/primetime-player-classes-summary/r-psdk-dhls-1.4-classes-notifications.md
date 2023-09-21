---
description: 這些類別會說明關於錯誤、警告和某些活動的訊息，這些訊息會這些問題以用於記錄及偵錯。
title: 通知類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 通知類別 {#notification-classes}

這些類別會說明關於錯誤、警告和某些活動的訊息，這些訊息會這些問題以用於記錄及偵錯。

封裝： [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 類別名稱 | 說明 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供資訊性訊息、警告和錯誤的類別。 封裝單一通知事件的物件表示 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [通知代碼](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 傳回與提供的通知程式碼相關的說明，並提供通知物件的數值常數。 |
| [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 儲存通知物件記錄的類別。 循環清單，其中 [NotificationhistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) 提供通知事件歷史記錄清單存取權的物件。 也就是說，它會維護一個元素清單，每個元素都包含個別的 [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) 類別。 |
| [NotificationhistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 定義中循環清單專案的類別 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) 並保留通知及其時間戳記。 |
| [通知型別](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含受支援通知型別的類別。 |
