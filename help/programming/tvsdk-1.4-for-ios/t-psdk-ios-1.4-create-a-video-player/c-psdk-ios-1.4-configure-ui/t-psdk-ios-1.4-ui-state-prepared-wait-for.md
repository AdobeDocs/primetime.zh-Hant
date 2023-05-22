---
description: 在您可以使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。
title: 等待有效狀態
exl-id: 150b37b8-c36d-4143-bead-ddc601bba6fe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 等待有效狀態{#wait-for-a-valid-state}

在您可以使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。

玩家在各種狀態中移動。 等待播放器處於正確狀態可確保媒體資源已成功載入。 如果玩家至少未處於所需狀態，則許多玩家方法會拋出 `IllegalStateException`。

所需狀態通常為 `PTMediaPlayerStatusReady`。
