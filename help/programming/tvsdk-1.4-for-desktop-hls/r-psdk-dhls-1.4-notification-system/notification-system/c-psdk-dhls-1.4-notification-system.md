---
description: MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
title: 播放器狀態、活動、錯誤和記錄的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 概述{#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊建立診斷和驗證的記錄系統。

您實作事件監聽器以擷取並回應事件。 許多事件都提供`MediaPlayerNotification`狀態通知。