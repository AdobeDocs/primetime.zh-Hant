---
description: 您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。
seo-description: 您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。
seo-title: 等待有效狀態
title: 等待有效狀態
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# 等待有效狀態{#wait-for-a-valid-state}

您必須先將播放器設為有效狀態，才能使用大部分的瀏覽器TVSDK播放器方法。

玩家會穿越各種狀態。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器至少未處於必要狀態，許多播放器方法會擲出`IllegalStateException`。

所需狀態通常為PREPARED。

1. 要確認狀態為「已準備」，請執行以下操作：

   當播放器初始化時，請等待瀏覽器TVSDK以`event.status`的`MediaPlayerStatus.PREPARED`發送`AdobePSDK.MediaPlayerStatusChangeEvent`事件。

   要檢查MediaPlayer對象的當前狀態是否至少為「已準備」。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

