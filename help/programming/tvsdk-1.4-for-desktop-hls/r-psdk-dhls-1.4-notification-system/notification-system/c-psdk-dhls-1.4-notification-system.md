---
description: MediaPlayerNotification對象提供有關播放器狀態、警告和錯誤更改的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。
title: 播放器狀態、活動、錯誤和記錄的通知
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 概述 {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification對象提供有關播放器狀態、警告和錯誤更改的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。

您的應用程式可以檢索通知和狀態資訊。 您還可以使用通知資訊建立診斷和驗證的日誌記錄系統。

實現事件偵聽器以捕獲和響應事件。 許多事件提供 `MediaPlayerNotification` 狀態通知。
