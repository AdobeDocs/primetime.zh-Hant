---
description: 在您可以使用大多數瀏覽器TVSDK播放器方法之前，播放器必須處於有效狀態。
title: 等待有效狀態
exl-id: 14f6a5db-4f81-448b-b291-487569a7bc4e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# 等待有效狀態 {#wait-for-a-valid-state}

在您可以使用大多數瀏覽器TVSDK播放器方法之前，播放器必須處於有效狀態。

玩家通過各種狀態。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家至少未處於所需狀態，則許多玩家方法會拋出 `IllegalStateException`。

所需狀態通常為PREPARED。

1. 要確認狀態為PREPARED:

   播放器初始化時，等待瀏覽器TVSDK派單 `AdobePSDK.MediaPlayerStatusChangeEvent` 事件 `event.status` 共 `MediaPlayerStatus.PREPARED`。

   檢查MediaPlayer對象的當前狀態是否至少為PREPARED。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
