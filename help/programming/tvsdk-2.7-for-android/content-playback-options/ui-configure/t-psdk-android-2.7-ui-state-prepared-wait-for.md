---
description: 您必須先讓播放器處於有效狀態，才能使用大部分的TVSDK播放器方法。
title: 等待有效的狀態
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-state}

透過TVSDK，您可以控制即時和隨選視訊(VOD)的基本播放體驗。 TVSDK提供播放器例項上的方法與屬性，供您設定播放器使用者介面。

您必須先讓播放器處於有效狀態，才能使用大部分的TVSDK播放器方法。

等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `MediaPlayerException`.

所需的狀態通常是「已準備」。 發生此情況時，的回呼常式 `StatusChangeEventListener.onStatusChanged()` 執行。

1. 若要確認狀態為 `PREPARED`，檢查 `MediaPlayer.MediaPlayerStatus`.
