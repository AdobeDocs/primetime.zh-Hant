---
description: 當使用者在媒體中快速前進或快速倒帶時，他們處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
title: 實作快速前進和倒帶
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 實作快速前進和倒帶 {#implement-fast-forward-and-rewind}

當使用者在媒體中快速前進或快速倒帶時，他們處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。

若要切換速度，您必須設定一個值。

1. 設定「 」，從一般播放模式(1x)移至特技播放模式 `rate` 上的屬性 `MediaPlayer` 至允許的值。

   * 此 `MediaPlayerItem` 類別會定義允許的播放速率。
   * 如果不允許指定的速率，TVSDK會選取最接近的允許速率。

      當點按播放速率從0 （暫停）或1 （正常播放）變更為大於1或小於–1的速率時，時間軸上的所有廣告都會被移除。 整個時間軸上只有一個句號，可促進點選播放，讓內容能夠快速轉送和倒帶，而不會在任何廣告位置停止。 此動作會由TVSDK上的時間軸分離動作啟用，以移除所有已解析的廣告插播。 在0或1處繼續播放trickplay時，會先透過時間軸附件動作還原adBreak。

      請記住以下資訊：

   * 如果點按播放動作是倒帶內容，則播放會在速率變更為1時繼續。
   * 如果點按播放動作是快進內容，則最後一個略過的adBreak會在恢復位置播放。

   此範例會將播放器的內部播放速率設定為要求的速率。

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 您可以選擇接聽費率變更事件，讓您知道何時要求費率變更，以及實際發生費率變更的時間。

   TVSDK會傳送以下與特技播放相關的事件：

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 當 `rate` 值會變更為其他值。

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 以選取的速率繼續播放時。

   當播放器從特技播放模式返回正常播放模式時，TVSDK會傳送這兩個事件。

## 費率變更API元素 {#rate-change-api}

TVSDK包含方法、屬性和事件，用於決定有效率、目前率、是否支援特技播放，以及與快速前進和倒帶相關的其他功能。

使用下列API元素來變更播放率：

* `MediaPlayer.rate` 具有setter和getter函式的屬性
* `MediaPlayer.localTime property` 使用getter函式
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` 具有getter函式的屬性
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` 屬性搭配getter函式 — 指定有效速率。

| 費率值 | 播放效果 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | 使用指定的乘數切換到快進模式，速度比正常快（例如，4比正常快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | 切換至快速倒帶模式 |
| 1.0 | 切換到一般播放模式(呼叫 `play` 與將rate屬性設定為1.0相同) |
| 0.0 | 暫停（呼叫） `pause` 與將rate屬性設定為0.0相同) |

## 特技播放的限制和行為 {#limitations-behavior-trick-play}

以下是特技播放模式的限制：

* 主播放清單必須包含I-frame-only區段。 熒幕上只會顯示I影格軌跡的關鍵影格。
* 音軌和隱藏式字幕已停用。
* 最適化位元速率(ABR)邏輯已停用。 TVSDK會選取最低提供速率與800 kbps之間的位元速率，並在整個特技播放工作階段中使用該速率。
* 已啟用播放和暫停。
* 不允許搜尋。 若要搜尋，請呼叫 `pause` 結束特技播放模式，然後呼叫 `seek`.

* 您可以退出特技播放模式，進入任何允許的播放速率（播放或暫停）。
* 將廣告整合到串流中時：

   * 您只能在播放主要內容時玩技巧。 如果您嘗試在廣告插播期間切換為特技播放，則會傳送錯誤。
   * 開始特技播放模式後，會忽略廣告插播且不會引發任何廣告事件。
   * 即使略過廣告插播，TVSDK向播放器應用程式公開的時間軸也不會修改。
   * 此 `MediaPlayer.currentTime` 屬性會隨著略過的廣告插播的持續時間向前跳轉（快進）或向後跳轉（快退）。 此目前時間的跳轉行為可讓串流持續時間在特技播放期間保持未修改。 您的播放器應用程式可使用 `localTime` 屬性，僅追蹤相對於主要內容的時間。 略過廣告時，不會對傳回的當地時間值執行時間跳躍。

   * 此 `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` 緊接在即將略過廣告插播之前傳送事件。 您的播放器可使用此事件來實作與已略過廣告插播相關的自訂邏輯。
   * 結束特技播放會叫用與結束搜尋時相同的廣告播放原則。

      因此，如同搜尋一樣，行為取決於應用程式的播放原則是否與預設值不同。 預設為上次略過的廣告插播會在您結束特技播放時播放。
