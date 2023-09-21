---
description: 您必須先讓播放器處於有效狀態，才能使用大部分的TVSDK播放器方法。
title: 等待有效的狀態
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-state}

透過TVSDK，您可以控制即時和隨選視訊(VOD)的基本播放體驗。 TVSDK提供播放器例項上的方法與屬性，可用來設定播放器使用者介面。在使用大部分TVSDK播放器方法之前，播放器必須處於有效狀態。

播放器會移動各種狀態。 等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `IllegalStateException`.

所需的狀態通常是「已準備」。

1. 若要確認狀態為「已準備」，請執行下列動作：

   當播放器初始化時，請等候TVSDK呼叫 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 狀態為「已準備」的事件。

   若要檢查目前的狀態 `MediaPlayer` 物件至少已準備好。

   ```
   function getstatus():String;
   ```
