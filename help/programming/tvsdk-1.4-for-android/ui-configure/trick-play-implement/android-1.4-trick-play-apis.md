---
description: TVSDK包含可判斷有效率、目前率、特技播放是否受支援以及其他與快進和倒轉相關功能的方法、屬性和事件。
seo-description: TVSDK包含可判斷有效率、目前率、特技播放是否受支援以及其他與快進和倒轉相關功能的方法、屬性和事件。
seo-title: 比率變更API元素
title: 比率變更API元素
uuid: 0040d35c-f9cb-4066-9bee-828ed5541194
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# 變速API元素{#rate-change-api-elements}

TVSDK包含可判斷有效率、目前率、特技播放是否受支援以及其他與快進和倒轉相關功能的方法、屬性和事件。

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

使用下列API元素來變更播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates` -指定有效率。

| 比率值 | 播放效果 |
|---|---|
| 2.0、4.0、8.0、16.0、32.0、64.0、128.0 | 切換到快進模式時，指定的乘數比正常速度快（例如，4比正常速度快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | 切換為快回風模式 |
| 1.0 | 切換為正常播放模式（呼叫`play`與將速率屬性設為1.0相同） |
| 0.0 | 暫停（呼叫`pause`與將rate屬性設為0.0相同） |

