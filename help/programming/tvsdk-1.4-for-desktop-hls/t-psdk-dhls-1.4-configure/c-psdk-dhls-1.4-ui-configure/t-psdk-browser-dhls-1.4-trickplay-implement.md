---
description: 當用戶快速前進或快速倒帶通過媒體時，他們處於特技播放模式。 要進入特技播放模式，您需要將MediaPlayer播放速率設定為1以外的值。
title: 快速前進和倒帶
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 快速前進和倒帶 {#implement-fast-forward-and-rewind}

當用戶快速前進或快速倒帶通過媒體時，他們處於特技播放模式。 要進入特技播放模式，您需要將MediaPlayer播放速率設定為1以外的值。

要切換速度，必須設定一個值。

1. 通過設定 `rate` 屬性 `MediaPlayer` 值。

   * 的 `MediaPlayerItem` 類定義允許的播放速率。
   * 如果不允許指定速率，TVSDK將選擇最接近的允許速率。

      當漸變播放率從0（暫停）或1（正常播放）更改為大於1或小於–1的速率時，將刪除時間線上的所有廣告。 整個時間線上只有一個週期，該週期便於變戲動作以允許內容被快速轉發和重繞，而不會停止在任何廣告位置。 此操作由TVSDK上的時間線拆分操作啟用，以刪除所有已解析的adBreaks。 在0或1時恢復特技播放時，adBreaks首先由時間線附加操作恢復。

      記住以下資訊：

   * 如果播放動作是倒帶內容，則當速率更改為1時，回放將恢復。
   * 如果要快速轉發內容，則上次跳過的adBreak將在恢復位置播放。

   此示例將播放器的內部播放速率設定為請求的速率。

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 您可以選擇偵聽匯率變動事件，這些事件會在您請求匯率變動時和實際發生匯率變動時通知您。

   TVSDK派送以下與特技播放相關的事件：

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 當 `rate` 值將更改為其他值。

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 以選定速率恢復播放時。

   當播放器從特技播放模式返回到正常播放模式時，TVSDK將調度這兩個事件。

## 速率更改API元素 {#rate-change-api}

TVSDK包括確定有效速率、當前速率、是否支援特技播放以及與快速轉發和倒帶相關的其他功能的方法、屬性和事件。

使用以下API元素更改播放率：

* `MediaPlayer.rate` 具有setter和getter函式的屬性
* `MediaPlayer.localTime property` 帶getter函式
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` 帶getter函式的屬性
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` 具有getter函式的屬性 — 指定有效的速率。

| 匯率值 | 對播放的影響 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | 切換到快進模式，使用指定的乘數比正常速度快（例如，4比正常速度快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | 切換到快速倒帶模式 |
| 1.0 | 切換到正常播放模式（呼叫） `play` 與將rate屬性設定為1.0相同) |
| 0.0 | 暫停（調用） `pause` 與將rate屬性設定為0.0相同) |

## 特技遊戲的限制和行為 {#limitations-behavior-trick-play}

以下是特技播放模式的限制：

* 主播放清單必須包含僅限I幀的段。 螢幕上只顯示I幀軌道中的關鍵幀。
* 禁用音頻軌道和隱藏字幕。
* 自適應位速率(ABR)邏輯被禁用。 TVSDK在最低提供速率和800 kbps之間選擇一個比特率，並在整個特技播放會話期間使用該速率。
* 已啟用播放和暫停。
* 不允許查找。 要查找，請撥打 `pause` 退出特技播放模式，然後 `seek`。

* 您可以將特技播放模式退出到任何允許的播放速率（播放或暫停）。
* 在流中加入廣告時：

   * 你只能在播放主要內容時玩特技遊戲。 如果您嘗試在廣告中斷期間切換到特技播放，則會發出錯誤。
   * 在開始特技播放模式後，忽略廣告中斷，並且不觸發廣告事件。
   * 即使跳過廣告中斷，TVSDK向播放器應用程式公開的時間線也不會被修改。
   * 的 `MediaPlayer.currentTime` 屬性在跳過和中斷的持續時間內向前（在快進時）或向後（在快退時）跳轉。 當前時間的這種跳轉行為允許在特技播放期間保持流持續時間不變。 您的播放器應用程式可以使用 `localTime` 屬性，以僅跟蹤主內容的時間。 跳過廣告時，不會對為本地時間返回的值執行時間跳轉。

   * 的 `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` 在即將跳過廣告中斷之前立即調度事件。 您的播放器可以使用此事件實現與跳過的廣告中斷相關的自定義邏輯。
   * 退出特技播放會調用與退出搜索時相同的廣告播放策略。

      因此，與查找一樣，行為取決於應用程式的回放策略是否與預設策略不同。 預設情況是，最後一次跳過的廣告時段在您結束特技播放時播放。
