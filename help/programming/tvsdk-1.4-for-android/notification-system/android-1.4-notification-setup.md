---
description: 您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。
seo-description: 您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。
seo-title: 設定通知系統
title: 設定通知系統
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 設定通知系統{#set-up-your-notification-system}

您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。

Primetime Player通知系統的核心是`Notification`類別，代表獨立通知。

`NotificationHistory`類別提供累積通知的機制。 它會儲存代表通知集合的通知記錄(NotificationHistoryItem)物件。

若要接收通知：

* 監聽通知
* 新增通知至通知歷史記錄

1. 監聽狀態變更。
1. 實作`MediaPlayer.PlaybackEventListener.onStateChanged`回呼。
1. TVSDK會傳遞兩個參數至回呼：

   * 新狀態(`MediaPlayer.PlayerState`)
   * `MediaPlayerNotification`物件

