---
description: 在您可以使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。
title: 等待有效狀態
exl-id: bfd77163-7ca8-41e1-8b97-2d6a765f5ccd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 等待有效狀態 {#wait-for-a-valid-status}

使用TVSDK，您可以控制即時視頻點播(VOD)的基本播放體驗。 TVSDK提供了播放器實例上可用於配置播放器用戶介面的方法和屬性。

在您可以使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。

等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家至少未處於所需狀態，則許多玩家方法會拋出 `MediaPlayerException`。

所需狀態通常為PREPARED。 出現這種情況時，的回調常式 `StatusChangeEventListener.onStatusChanged()` 執行。

確認狀態為 `PREPARED`選中 `MediaPlayer.MediaPlayerStatus`。
