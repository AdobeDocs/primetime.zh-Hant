---
description: 這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。
seo-description: 這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。
seo-title: 通知類
title: 通知類
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 通知類{#notification-classes}

這些類別說明有關錯誤、警告和某些活動的訊息，而TVSDK會針對登入和除錯而發出問題。

套件： [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) Package: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 類別名稱 | 說明 |
|---|---|
| MediaPlayerNotification。 [錯誤](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 說明導致播放器停止播放之錯誤通知的類別。 這是通知 [類型為](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) ERROR的MediaPlayerNotification。 |
| MediaPlayerNotification。 [資訊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 說明資訊通知的類。 這是通知 [類型](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) INFO的MediaPlayerNotification。 |
| MediaPlayerNotification。 [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 說明警告通知的類別。 這是通知 [類型為](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) WARNING的MediaPlayerNotification。 |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 提供資訊性消息、警告和錯誤的類。 封裝 [NotificationHistory中單一通知事件的物件表示](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html)。 |
| MediaPlayerNotification。 [通知代碼](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 傳回與所提供之通知程式碼相關聯的說明。 |
| [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 儲存通知對象日誌的類。 NotificationHistory.Item [對象的循環清單](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) ，它提供對通知事件歷史記錄清單的訪問。 也就是說，它會維護元素清單，每個元素都包含 [MediaPlayerNotification類別的個別例項](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 。 (在會 [話包中](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 。) |
| 通知歷史記錄。 [項目](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | 在 [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) NotificationHistory中定義循環清單中條目並保存通知及其時間戳的類。 |
| MediaPlayerNotification。 [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 包含支援通知類型的類別。 |