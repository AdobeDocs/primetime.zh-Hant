---
description: 您可以監聽通知，也可以將您自己的通知新增至通知歷史記錄。
title: 設定您的通知系統
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 設定您的通知系統{#set-up-your-notification-system}

您可以監聽通知，也可以將您自己的通知新增至通知歷史記錄。

Primetime播放器通知系統的核心為 `Notification` 類別，代表獨立通知。

此 `NotificationHistory` class提供累積通知的機制。 它會儲存代表通知集合的通知(NotificationHistoryItem)物件的記錄。

若要接收通知：

* 接聽通知
* 將通知新增至通知歷史記錄

1. 接聽狀態變更。
1. 實作 `MediaPlayer.PlaybackEventListener.onStateChanged` callback。
1. TVSDK會將兩個引數傳遞至回呼：

   * 新狀態( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 物件

