---
description: 在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。
seo-description: 在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。
seo-title: 等待有效狀態
title: 等待有效狀態
uuid: e13201d7-b217-4d01-bdb7-a71855e3500e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 等待有效狀態{#wait-for-a-valid-state}

在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。

玩家會移動各種狀態。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家至少未處於必要狀態，會擲出許多玩家方法 `IllegalStateException`。

所需狀態通常為 `PTMediaPlayerStatusReady`。
