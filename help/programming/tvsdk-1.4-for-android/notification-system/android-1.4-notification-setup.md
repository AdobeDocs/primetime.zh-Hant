---
description: 您可以監聽通知，也可以將自己的通知添加到通知歷史記錄中。
title: 設定通知系統
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 設定通知系統{#set-up-your-notification-system}

您可以監聽通知，也可以將自己的通知添加到通知歷史記錄中。

黃金時段播放器通知系統的核心是 `Notification` 類，表示獨立通知。

的 `NotificationHistory` 類提供了累計通知的機制。 它儲存表示通知集合的通知日誌(NotificationHistoryItem)對象。

要接收通知，請執行以下操作：

* 偵聽通知
* 將通知添加到通知歷史記錄

1. 偵聽狀態更改。
1. 實施 `MediaPlayer.PlaybackEventListener.onStateChanged` 回叫。
1. TVSDK將兩個參數傳遞給回調：

   * 新狀態( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 對象

