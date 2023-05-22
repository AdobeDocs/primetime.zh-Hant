---
description: 這些類描述有關錯誤、警告和TVSDK為記錄和調試而發出的某些活動的消息。
title: 通知類
exl-id: b869c201-2731-42e5-a20e-282edd2caddc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 通知類{#notification-classes}

這些類描述有關錯誤、警告和TVSDK為記錄和調試而發出的某些活動的消息。

包： [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  包： [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 類名 | 說明 |
|---|---|
| MediaPlayerNotification。 [錯誤](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 描述導致播放器停止播放的錯誤通知的類。 這是 [媒體播放器通知](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知類型ERROR。 |
| MediaPlayerNotification。 [資訊](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 描述資訊通知的類。 這是 [媒體播放器通知](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知類型INFO。 |
| MediaPlayerNotification。 [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 描述警告通知的類。 這是 [媒體播放器通知](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知類型WARNING。 |
| [媒體播放器通知](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 提供資訊性消息、警告和錯誤的類。 封裝中單個通知事件的對象表示 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html)。 |
| MediaPlayerNotification。 [通知代碼](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 返回與提供的通知代碼關聯的說明。 |
| [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 儲存通知對象日誌的類。 循環清單 [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 提供對通知事件歷史記錄清單的訪問的對象。 即，它維護一個元素清單，每個元素都包含 [媒體播放器通知](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 類。 (在 [會話](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 包。) |
| 通知歷史記錄。 [物料](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | 在循環清單中定義條目的類 [通知歷史記錄](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) 並保存通知及其時間戳。 |
| MediaPlayerNotification。 [條目類型](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 包含支援的通知類型的類。 |
