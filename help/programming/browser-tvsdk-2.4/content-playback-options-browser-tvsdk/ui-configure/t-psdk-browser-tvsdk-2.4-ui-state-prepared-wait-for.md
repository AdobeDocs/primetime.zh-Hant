---
description: 您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。
seo-description: 您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。
seo-title: 等待有效狀態
title: 等待有效狀態
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 等待有效狀態 {#wait-for-a-valid-state}

您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。

玩家會穿越各種狀態。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家未處於至少必要的狀態，會擲出許多玩家方法 `IllegalStateException`。

所需狀態通常為PREPARED。

1. 要確認狀態為「已準備」，請執行以下操作：

   當播放器正在初始化時，請等待瀏覽器TVSDK以 `AdobePSDK.MediaPlayerStatusChangeEvent` 下列字元分派 `event.status` 事件 `MediaPlayerStatus.PREPARED`。

   要檢查MediaPlayer對象的當前狀態是否至少為「已準備」。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

