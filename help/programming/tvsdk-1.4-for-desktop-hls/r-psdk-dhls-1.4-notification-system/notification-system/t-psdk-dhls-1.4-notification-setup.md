---
description: 您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。
seo-description: 您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。
seo-title: 設定通知系統
title: 設定通知系統
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# 設定通知系統{#set-up-your-notification-system}

您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。

Primetime Player通知系統的核心是Notification類別，它代表獨立通知。

NotificationHistory類提供累積通知的機制。 它儲存表示通知集合的通知(`NotificationHistoryItem`)對象日誌。

若要接收通知：

* 監聽通知
* 新增通知至通知歷史記錄

1. 監聽狀態變更。
1. 實作`MediaPlayer.StatusChangeEvent.STATUS_CHANGED`事件偵聽器。
1. TVSDK會將`MediaPlayer.StatusChangeEvent`例項傳遞至事件偵聽器，其中包含兩個參數：

   * 新狀態(`MediaPlayer.Status`)
   * `MediaPlayerNotification`物件

