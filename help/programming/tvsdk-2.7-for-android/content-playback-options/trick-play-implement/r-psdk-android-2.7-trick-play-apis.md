---
description: TVSDK包括確定有效速率、當前速率、是否支援特技播放以及與快速轉發和倒帶相關的其他功能的方法、屬性和事件。
title: 速率更改API元素
exl-id: deb8c1cb-c6b2-4328-a5e1-cca893ea066f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 速率更改API元素 {#rate-change-api-elements}

TVSDK包括確定有效速率、當前速率、是否支援特技播放以及與快速轉發和倒帶相關的其他功能的方法、屬性和事件。

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

使用以下API元素更改播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`，它指定有效率。

| 匯率值 | 對播放的影響 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 切換到快進模式，使用指定的乘數比正常速度快（例如，4比正常速度快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 切換到快速倒帶模式 |
| 1.0 | 切換到正常播放模式（呼叫） `play` 與將rate屬性設定為1.0相同) |
| 0.0 | 暫停（調用） `pause` 與將rate屬性設定為0.0相同) |
