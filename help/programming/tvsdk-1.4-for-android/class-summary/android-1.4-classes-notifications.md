---
description: 這些類別會說明TVSDK為了記錄與偵錯目的而發出的錯誤、警告和一些活動的相關訊息。
title: 通知類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 通知類別{#notification-classes}

這些類別會說明TVSDK為了記錄與偵錯目的而發出的錯誤、警告和一些活動的相關訊息。

封裝： [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  封裝： [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 類別名稱 | 說明 |
|---|---|
| MediaPlayerNotification。 [錯誤](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 描述導致播放器停止播放的錯誤通知類別。 這是 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 的通知型別ERROR。 |
| MediaPlayerNotification。 [資訊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 說明資訊性通知的類別。 這是 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知型別INFO的。 |
| MediaPlayerNotification。 [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 說明警告通知的類別。 這是 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知型別WARNING的。 |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 提供資訊性訊息、警告和錯誤的類別。 封裝單一通知事件的物件表示 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification。 [通知代碼](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 傳回與提供的通知代碼相關的說明。 |
| [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 儲存通知物件記錄的類別。 循環清單，其中 [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 提供通知事件歷史記錄清單存取權的物件。 也就是說，它會維護一個元素清單，每個元素都包含個別的 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 類別。 (在 [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 封裝。) |
| Notificationhistory。 [專案](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | 定義中循環清單專案的類別 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) 並保留通知及其時間戳記。 |
| MediaPlayerNotification。 [專案型別](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 包含受支援通知型別的類別。 |
