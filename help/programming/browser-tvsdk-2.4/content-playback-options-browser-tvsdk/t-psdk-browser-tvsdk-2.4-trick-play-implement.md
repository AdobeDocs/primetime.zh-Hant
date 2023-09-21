---
description: 當使用者在媒體中快速前進或快速倒帶時，他們處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
title: 實作快速前進和倒帶
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 實作快速前進和倒帶{#implement-fast-forward-and-rewind}

當使用者在媒體中快速前進或快速倒帶時，他們處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。

>[!IMPORTANT]
>
>* 僅MPEG短劃線和HLS VOD內容支援特技播放模式。
>* 即時資料流或廣告不支援特技播放模式。
>* 從主要內容切換至廣告時，瀏覽器TVSDK會維持特技播放模式。
>

若要切換速度，您必須設定一個值。

1. 從一般播放模式(1x)移至特技播放模式，方法是在 `MediaPlayer` 至允許的值。

   * 此 `MediaPlayerItem` 類別會定義允許的播放速率。
   * 如果不允許指定的速率，瀏覽器TVSDK會選取最接近的允許速率。

     下列範例函式會設定速率：

     ```js
     setTrickPlayRate = function (player, trickPlayRate) { 
                   player.rate = trickPlayRate; 
     }
     ```

     以下範例函式可用於查詢可用的播放速率：

     ```js
     getAvailableTrickPlayRates = function (player) { 
              var item = player.currentItem; 
              var availableRates = item. availablePlaybackRates; 
              return availableRates; 
     } 
     ```

1. 您可以選擇接聽費率變更事件，讓您知道何時要求費率變更，以及實際發生費率變更的時間。

       瀏覽器TVSDK會傳送下列與特技播放相關的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 當 `rate` 值會變更為其他值。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以選取的速率繼續播放時。

     當播放器從特技播放模式返回正常播放模式時，瀏覽器TVSDK會傳送這兩個事件。

## 費率變更API元素 {#rate-change-API-elements}

瀏覽器TVSDK包含方法、屬性和事件，用於決定有效速率、目前速率、是否支援特技播放，以及與快速前進和倒帶相關的其他功能。

使用下列API元素來變更播放率：

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates`  — 指定有效費率。

  | 費率值 | 播放效果 |
  |---|---|
  | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | 使用指定的乘數切換到快轉模式，速度比正常快（例如，4比正常快4倍） |
  | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | 切換至快速倒帶模式 |
  | 1.0 | 切換到一般播放模式(呼叫 `play` 與將rate屬性設定為1.0相同) |
  | 0.0 | 暫停（呼叫） `pause` 與將rate屬性設為0.0相同) |

## 特技播放的限制和行為 {#limitations-and-behavior-trick-play}

特技播放模式的運作方式有一些限制和問題。

以下是特技播放模式限制的清單：

* 如果串流未包含特技播放適配，則會停用快速倒帶，而且快進的最大播放速率限製為8。
* 當使用特技播放調整提供特技模式時，音軌會停用。
* 在特技播放模式中，會停用音訊和隱藏式字幕曲目的切換。
* 播放和暫停已啟用。
* 在搜尋時，如果播放處於特技播放模式，則播放速率會設為1並繼續正常播放。
* 已啟用最適化位元速率(ABR)邏輯。

  使用一般調整時，設定檔會限制在 `ABRControlParameters.minBitRate` 和 `ABRControlParameters.maxBitRate`. 當使用特技播放調整時，設定檔被限制在 `ABRControlParameters.minTrickPlayBitRate` 和 `ABRControlParameters.maxTrickPlayBitRate`.
