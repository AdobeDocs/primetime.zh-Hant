---
description: MediaPlayerNotification物件提供有關播放器狀態變更、警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態變更。
title: 播放器狀態、活動、錯誤和記錄的通知
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 概觀 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification物件提供有關播放器狀態變更、警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊，建立用於診斷和驗證的記錄系統。

您可以實作事件接聽程式來擷取和回應事件。 許多事件提供 `MediaPlayerNotification` 狀態通知。
