---
description: 您必須先將播放器設為有效狀態，才能使用大部分的TVSDK播放器方法。
title: 等待有效的狀態
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 等待有效的狀態 {#wait-for-a-valid-state}

透過TVSDK，您可以控制即時和隨選視訊(VOD)的基本播放體驗。 TVSDK提供播放器例項上的方法和屬性，可用於設定播放器使用者介面。在使用大多數TVSDK播放器方法之前，播放器必須處於有效狀態。

播放器會移動各種狀態。 等候播放器處於正確狀態可確保媒體資源已成功載入。 如果播放器未處於至少必要的狀態，許多播放器方法會擲回 `IllegalStateException`.

所需的狀態通常是PREPARED。

1. 若要確認狀態為「已準備」，請執行下列動作：

   播放器初始化時，請等待TVSDK呼叫 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有PREPARED狀態的事件。

   若要檢查的目前狀態 `MediaPlayer` 物件至少已準備就緒。

   ```
   function getstatus():String;
   ```
