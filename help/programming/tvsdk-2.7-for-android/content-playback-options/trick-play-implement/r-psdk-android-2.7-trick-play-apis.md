---
description: TVSDK包含方法、屬性和事件，用於判斷有效率、目前率、是否支援特技播放，以及與快速前進和倒退相關的其他功能。
title: 費率變更API元素
exl-id: deb8c1cb-c6b2-4328-a5e1-cca893ea066f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 費率變更API元素 {#rate-change-api-elements}

TVSDK包含方法、屬性和事件，用於判斷有效率、目前率、是否支援特技播放，以及與快速前進和倒退相關的其他功能。

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

使用下列API元素來變更播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`，會指定有效費率。

| 費率值 | 播放效果 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 使用指定的乘數切換到快進模式，速度比正常快（例如，4比正常快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 切換至快速倒帶模式 |
| 1.0 | 切換到一般播放模式(呼叫 `play` 與將rate屬性設定為1.0相同) |
| 0.0 | 暫停（呼叫） `pause` 與將rate屬性設定為0.0相同) |
