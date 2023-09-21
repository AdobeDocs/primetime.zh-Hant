---
description: 您必須先讓播放器處於有效狀態，才能使用大部分的TVSDK播放器方法。
title: 等待有效的狀態
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 等待有效的狀態{#wait-for-a-valid-state}

您必須先讓播放器處於有效狀態，才能使用大部分的TVSDK播放器方法。

播放器會移動各種狀態。 等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `IllegalStateException`.

所需的狀態通常是 `PTMediaPlayerStatusReady`.
