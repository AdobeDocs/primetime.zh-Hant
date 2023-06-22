---
description: 播放器必須處於有效狀態，您才能使用大部分的瀏覽器TVSDK播放器方法。
title: 等待有效的狀態
exl-id: 14f6a5db-4f81-448b-b291-487569a7bc4e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-state}

播放器必須處於有效狀態，您才能使用大部分的瀏覽器TVSDK播放器方法。

播放器會經過各種狀態。 等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `IllegalStateException`.

所需的狀態通常是PREPARED。

1. 若要確認狀態已準備就緒，請執行下列動作：

   播放器初始化時，請等候瀏覽器TVSDK派送 `AdobePSDK.MediaPlayerStatusChangeEvent` 具有的事件 `event.status` 之 `MediaPlayerStatus.PREPARED`.

   檢查MediaPlayer物件的目前狀態是否至少為PREPARED。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
