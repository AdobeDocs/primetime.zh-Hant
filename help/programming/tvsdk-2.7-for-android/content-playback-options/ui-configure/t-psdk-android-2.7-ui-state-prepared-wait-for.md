---
description: 在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。
seo-description: 在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。
seo-title: 等待有效狀態
title: 等待有效狀態
uuid: ffa63ad6-84d3-4eb2-aa99-026418d86528
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 等待有效狀態 {#wait-for-a-valid-state}

有了TVSDK，您就可以控制即時和隨選視訊(VOD)的基本播放體驗。 TVSDK提供播放器例項上的方法和屬性，供您用來設定播放器使用者介面。

在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。

等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家至少未處於必要狀態，會擲出許多玩家方法 `MediaPlayerException`。

所需狀態通常為「已準備」。 發生此情況時，將執行回呼 `StatusChangeEventListener.onStatusChanged()` 常式。

1. 要確認狀態為，請 `PREPARED`選中 `MediaPlayer.MediaPlayerStatus`。
