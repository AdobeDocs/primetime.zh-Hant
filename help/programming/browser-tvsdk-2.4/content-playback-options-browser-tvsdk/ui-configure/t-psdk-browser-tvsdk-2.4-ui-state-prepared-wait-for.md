---
description: 您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。
title: 等待有效的狀態
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-state}

您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。

播放器會經過各種狀態。 等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `IllegalStateException`.

所需的狀態通常是「已準備」。

1. 若要確認狀態已準備就緒，請執行下列動作：

   當播放器初始化時，請等待瀏覽器TVSDK傳送 `AdobePSDK.MediaPlayerStatusChangeEvent` 事件與 `event.status` 之 `MediaPlayerStatus.PREPARED`.

   檢查MediaPlayer物件的目前狀態是否至少為PREPARED。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
