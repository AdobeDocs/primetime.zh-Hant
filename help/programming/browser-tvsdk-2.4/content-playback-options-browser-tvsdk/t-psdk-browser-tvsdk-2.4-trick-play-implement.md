---
description: 當用戶快速前進或快速倒帶通過媒體時，他們處於特技播放模式。 要進入特技播放模式，您需要將MediaPlayer播放速率設定為1以外的值。
title: 快速前進和倒帶
exl-id: 21f9a3f6-1cae-4240-991d-c03a0e49adf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 快速前進和倒帶{#implement-fast-forward-and-rewind}

當用戶快速前進或快速倒帶通過媒體時，他們處於特技播放模式。 要進入特技播放模式，您需要將MediaPlayer播放速率設定為1以外的值。

>[!IMPORTANT]
>
>* 特技播放模式僅支援MPEG Dash和HLS VOD內容。
>* 即時流或廣告不支援特技播放模式。
>* 當從主內容切換到廣告時，瀏覽器TVSDK會離開特技播放模式。
>


要切換速度，必須設定一個值。

1. 通過設定正常播放模式(1x)上的速率，從特技播放模式移動到特技播放模式 `MediaPlayer` 值。

   * 的 `MediaPlayerItem` 類定義允許的播放速率。
   * 如果不允許指定速率，則瀏覽器TVSDK將選擇最接近的允許速率。

      以下示例函式設定速率：

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      以下示例函式可用於查詢可用的播放速率：

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. 您可以選擇偵聽匯率變動事件，這些事件會在您請求匯率變動時和實際發生匯率變動時通知您。

       瀏覽器TVSDK調度以下與特技播放相關的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 當 `rate` 值將更改為其他值。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以選定速率恢復播放時。

      當播放器從特技播放模式返回到正常播放模式時，瀏覽器TVSDK調度這兩個事件。

## 速率更改API元素 {#rate-change-API-elements}

瀏覽器TVSDK包括確定有效速率、當前速率、是否支援特技播放以及與快速轉發和倒帶相關的其他功能的方法、屬性和事件。

使用以下API元素更改播放率：

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates`  — 指定有效的費率。

   | 匯率值 | 對播放的影響 |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | 切換到快進模式，使用指定的乘數比正常速度快（例如，4比正常速度快4倍） |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | 切換到快速倒帶模式 |
   | 1.0 | 切換到正常播放模式（呼叫） `play` 與將rate屬性設定為1.0相同) |
   | 0.0 | 暫停（調用） `pause` 與將rate屬性設定為0.0相同) |

## 特技遊戲的限制和行為 {#limitations-and-behavior-trick-play}

特技播放模式的行為方式存在一些局限性和問題。

下面是特技播放模式限制的清單：

* 如果該流不包含特技播放適配，則禁用快速倒帶，並且快進的最大播放速率限制為8。
* 當使用特技播放適應來提供特技模式時，禁用音頻軌道。
* 在特技播放模式中，禁用音頻和閉合字幕軌道的切換。
* 已啟用播放和暫停。
* 在尋道時，如果回放處於特技播放模式，則回放速率設定為1，並恢復正常回放。
* 啟用自適應比特率(ABR)邏輯。

   使用常規調整時，配置檔案將限制在 `ABRControlParameters.minBitRate` 和 `ABRControlParameters.maxBitRate`。 當使用特技遊戲改編時，配置檔案被限制在 `ABRControlParameters.minTrickPlayBitRate` 和 `ABRControlParameters.maxTrickPlayBitRate`。
