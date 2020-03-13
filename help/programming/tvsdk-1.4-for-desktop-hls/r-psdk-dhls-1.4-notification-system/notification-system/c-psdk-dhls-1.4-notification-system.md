---
description: MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
seo-description: MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
seo-title: 播放器狀態、活動、錯誤和記錄的通知
title: 播放器狀態、活動、錯誤和記錄的通知
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概觀 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊建立診斷和驗證的記錄系統。

您實作事件監聽器以擷取並回應事件。 許多事件都會提 `MediaPlayerNotification` 供狀態通知。