---
description: 您必須先將播放器設為有效狀態，才能使用大部分的TVSDK播放器方法。
title: 等待有效的狀態
exl-id: bfd77163-7ca8-41e1-8b97-2d6a765f5ccd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-status}

透過TVSDK，您可以控制即時和隨選視訊(VOD)的基本播放體驗。 TVSDK提供播放器例項上的方法和屬性，可用來設定播放器使用者介面。

您必須先將播放器設為有效狀態，才能使用大部分的TVSDK播放器方法。

等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `MediaPlayerException`.

所需的狀態通常是PREPARED。 發生此情況時，的回呼常式 `StatusChangeEventListener.onStatusChanged()` 執行。

若要確認狀態為 `PREPARED`，檢查 `MediaPlayer.MediaPlayerStatus`.
