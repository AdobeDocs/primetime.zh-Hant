---
description: 您可以監聽通知，也可以將您自己的通知新增至通知歷史記錄。
title: 設定您的通知系統
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 設定您的通知系統{#set-up-your-notification-system}

您可以監聽通知，也可以將您自己的通知新增至通知歷史記錄。

Primetime Player通知系統的核心是Notification類別，代表獨立通知。

NotificationHistory類別提供累積通知的機制。 它會儲存通知的記錄( `NotificationHistoryItem`)物件，代表通知的集合。

若要接收通知：

* 接聽通知
* 將通知新增至通知歷史記錄

1. 接聽狀態變更。
1. 實作 `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` 事件監聽器。
1. TVSDK傳遞 `MediaPlayer.StatusChangeEvent` 事件監聽器的執行處理，其中包含兩個引數：

   * 新狀態( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` 物件
