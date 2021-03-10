---
description: 在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。
title: 等待有效狀態
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 等待有效狀態{#wait-for-a-valid-state}

在您使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。

玩家會移動各種狀態。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器至少未處於必要狀態，許多播放器方法會擲出`IllegalStateException`。

所需狀態通常為`PTMediaPlayerStatusReady`。
