---
description: 您必須先將播放器設為有效狀態，才能使用大部分的TVSDK播放器方法。
title: 等待有效的狀態
exl-id: 2ea7e287-7393-4909-8f55-53cebf4dc289
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-state}

您必須先將播放器設為有效狀態，才能使用大部分的TVSDK播放器方法。

播放器會移動各種狀態。 等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `IllegalStateException`.

所需的狀態通常是 `PTMediaPlayerStatusReady`.
