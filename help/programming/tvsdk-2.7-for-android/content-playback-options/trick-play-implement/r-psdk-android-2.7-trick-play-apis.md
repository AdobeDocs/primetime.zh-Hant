---
description: TVSDK包含可判斷有效率、目前率、是否支援特技播放以及其他與快進和倒轉相關功能的方法、屬性和事件。
seo-description: TVSDK包含可判斷有效率、目前率、是否支援特技播放以及其他與快進和倒轉相關功能的方法、屬性和事件。
seo-title: 比率變更API元素
title: 比率變更API元素
uuid: 3554bf45-9419-4740-8a0e-484fc14c7436
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 比率變更API元素 {#rate-change-api-elements}

TVSDK包含可判斷有效率、目前率、是否支援特技播放以及其他與快進和倒轉相關功能的方法、屬性和事件。

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

使用下列API元素來變更播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`，指定有效率。

| 比率值 | 播放效果 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 切換到快進模式時，指定的乘數比正常速度快（例如，4比正常速度快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 切換為快回風模式 |
| 1.0 | 切換為正常播放模式( `play` 呼叫與將速率屬性設為1.0相同) |
| 0.0 | 暫停( `pause` 呼叫與將比率屬性設為0.0相同) |

