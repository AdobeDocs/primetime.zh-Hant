---
description: 當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
seo-description: 當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
seo-title: 實作快速前進和倒退
title: 實作快速前進和倒退
uuid: c1992757-d067-4c11-8d08-fec09099476f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 實作快速前進和倒退{#implement-fast-forward-and-rewind}

當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。

>[!IMPORTANT]
>
>* 特技播放模式僅支援MPEG Dash和HLS VOD內容。
>* 即時串流或廣告不支援特技播放模式。
>* 從主要內容切換至廣告時，瀏覽器TVSDK會保留特技播放模式。
>



要切換速度，必須設定一個值。

1. 將速率設為允許值，從正常播放模式(1x)移至特技 `MediaPlayer` 播放模式。

   * 類定 `MediaPlayerItem` 義允許的播放速率。
   * 若不允許指定比率，瀏覽器TVSDK會選取最接近的允許比率。

      以下示例函式設定比率：

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      下列範例函式可用來查詢可用的播放率：

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. 您可以選擇性地監聽費率變動事件，這些事件會在您請求費率變動時以及實際發生費率變動時告知您。

       瀏覽器TVSDK會記錄下列與特技播放相關的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 值變 `rate` 更為不同的值時。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 當播放以選取的速率繼續時。

      當播放器從特技播放模式返回正常播放模式時，瀏覽器TVSDK會調度這兩個事件。

## 比率變更API元素 {#rate-change-API-elements}

瀏覽器TVSDK包含方法、屬性和事件，以判斷有效率、目前比率、特技播放是否受支援，以及其他與快進和倒轉相關的功能。

使用下列API元素來變更播放率：

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` -指定有效率。

   | 比率值 | 播放效果 |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | 切換到快進模式時，指定的乘數比正常速度快（例如，4比正常速度快4倍） |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | 切換為快回風模式 |
   | 1.0 | 切換為正常播放模式( `play` 呼叫與將速率屬性設為1.0相同) |
   | 0.0 | 暫停( `pause` 呼叫與將比率屬性設為0.0相同) |

## 特技播放的限制和行為 {#limitations-and-behavior-trick-play}

特技播放模式的運作方式有一些限制和問題。

以下是特技播放模式限制的清單：

* 如果流不包含特技播放適配，則禁用快速倒轉，並且快進的最大播放速率限制為8。
* 當使用特技播放適應來提供特技模式時，音頻軌道被禁用。
* 在特技播放模式中，禁用音頻和隱藏字幕軌道的切換。
* 播放和暫停已啟用。
* 在尋道時，如果播放處於特技播放模式，則播放速率設為1，而正常播放繼續。
* 自適應位速率(ABR)邏輯被啟用。

   使用一般調整時，描述檔會限制在和 `ABRControlParameters.minBitRate` 之間 `ABRControlParameters.maxBitRate`。 當使用特技遊戲調整時，描述檔會限制在 `ABRControlParameters.minTrickPlayBitRate` 和之間 `ABRControlParameters.maxTrickPlayBitRate`。