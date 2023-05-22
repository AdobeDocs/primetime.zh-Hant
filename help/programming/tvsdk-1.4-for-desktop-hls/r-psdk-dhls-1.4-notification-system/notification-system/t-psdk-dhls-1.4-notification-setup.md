---
description: 您可以監聽通知，也可以將自己的通知添加到通知歷史記錄中。
title: 設定通知系統
exl-id: da6cec2d-8488-4f61-881b-72999ece650c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 設定通知系統{#set-up-your-notification-system}

您可以監聽通知，也可以將自己的通知添加到通知歷史記錄中。

Gimfige Player通知系統的核心是Notification類，它表示獨立通知。

NotificationHistory類提供了累計通知的機制。 它儲存通知日誌( `NotificationHistoryItem`)對象，它表示通知的集合。

要接收通知，請執行以下操作：

* 偵聽通知
* 將通知添加到通知歷史記錄

1. 偵聽狀態更改。
1. 實施 `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` 事件偵聽器。
1. TVSDK通過 `MediaPlayer.StatusChangeEvent` 事件偵聽器的實例，它包含兩個參數：

   * 新狀態( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` 對象
