---
description: 在您可以使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。
title: 等待有效狀態
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 等待有效狀態 {#wait-for-a-valid-state}

使用TVSDK，您可以控制即時視頻點播(VOD)的基本播放體驗。 TVSDK在播放器實例上提供了可用於配置播放器用戶介面的方法和屬性。在使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。

玩家在各種狀態中移動。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家至少未處於所需狀態，則許多玩家方法會拋出 `IllegalStateException`。

所需狀態通常為PREPARED。

1. 要確認狀態為「已準備」，請執行以下操作：

   播放器初始化時，等待TVSDK調用回調 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 狀態為PREPARED的事件。

   要檢查的當前狀態 `MediaPlayer` 對象至少為PREPARED。

   ```
   function getstatus():String;
   ```
