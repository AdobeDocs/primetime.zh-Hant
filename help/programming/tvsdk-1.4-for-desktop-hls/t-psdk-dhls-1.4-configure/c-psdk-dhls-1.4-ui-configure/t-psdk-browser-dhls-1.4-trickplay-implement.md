---
description: 當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。
title: 實作快速前進和倒退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# 實施快速前進和倒轉{#implement-fast-forward-and-rewind}

當使用者在媒體上快速前進或快速倒轉時，他們會處於特技播放模式。 若要進入特技播放模式，您必須將MediaPlayer播放速率設定為1以外的值。

要切換速度，必須設定一個值。

1. 將`MediaPlayer`上的`rate`屬性設定為允許的值，從一般播放模式(1x)移至特技播放模式。

   * `MediaPlayerItem`類別定義允許的播放速率。
   * 如果不允許指定速率，TVSDK會選取最接近的允許速率。

      當漸變播放率從0（暫停）或1（正常播放）變更為大於1或小於-1的速率時，時間軸上的所有廣告都會被移除。 整個時間軸上只有一個時段，可協助您執行特效動作，讓內容可快速轉送和重新卷繞，而不需停在任何廣告位置。 此動作由TVSDK上的時間軸分離動作啟用，以移除所有已解決的adBreaks。 在0或1繼續播放時，時間軸附件動作會先還原adBreaks。

      請記住下列資訊：

   * 如果特技播放動作是倒轉內容，當速率變更為1時，播放會繼續。
   * 如果要快速轉送內容的戲法動作，則最後一個跳過的adBreak會在繼續位置播放。

   此範例會將播放器的內部播放速率設為要求的速率。

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 您可以選擇性地監聽費率變動事件，這些事件會在您請求費率變動時以及實際發生費率變動時告知您。

   TVSDK記錄下列與特技播放相關的事件：

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 值變 `rate` 更為不同的值時。

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 當播放以選取的速率繼續時。

   當播放器從特技播放模式返回正常播放模式時，TVSDK會調度這兩個事件。

## 變速API元素{#rate-change-api}

TVSDK包含可判斷有效率、目前率、特技播放是否受支援以及其他與快進和倒轉相關功能的方法、屬性和事件。

使用下列API元素來變更播放率：

* `MediaPlayer.rate` 具有setter和getter函式的屬性
* `MediaPlayer.localTime property` 使用getter函式
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` 具有getter函式的屬性
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` property with getter函式——指定有效率。

| 比率值 | 播放效果 |
|---|---|
| 2.0、4.0、8.0、16.0、32.0、64.0、128.0 | 切換到快進模式時，指定的乘數比正常速度快（例如，4比正常速度快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | 切換為快回風模式 |
| 1.0 | 切換為正常播放模式（呼叫`play`與將速率屬性設為1.0相同） |
| 0.0 | 暫停（呼叫`pause`與將rate屬性設為0.0相同） |

## 特技播放的限制和行為{#limitations-behavior-trick-play}

以下是特技播放模式的限制：

* 主播放清單必須包含僅限I-frame的區段。 畫面上只會顯示I-frame音軌的關鍵影格。
* 音軌和隱藏字幕已停用。
* 自適應位速率(ABR)邏輯被禁用。 TVSDK會在最低提供速率和800 kbps之間選擇一個位元速率，並在整個特技播放階段作業期間使用該速率。
* 播放和暫停已啟用。
* 不允許搜尋。 若要尋找，請呼叫`pause`以退出特技播放模式，然後呼叫`seek`。

* 您可以將特技播放模式退出至任何允許的播放速率（播放或暫停）。
* 當廣告併入串流時：

   * 您只能在播放主要內容時去玩耍。 如果您嘗試在廣告中斷期間切換來設計播放，則會傳送錯誤。
   * 開始特技播放模式後，廣告插播會被忽略，且不會引發廣告事件。
   * 即使跳過廣告插播，TVSDK對播放器應用程式公開的時間軸也不會修改。
   * `MediaPlayer.currentTime`屬性會隨著跳過廣告插播的持續時間向前（在快進時）或向後（在快倒）跳過。 目前的這種跳轉行為允許在特技播放期間保留未修改的串流持續時間。 您的播放器應用程式可使用`localTime`屬性來追蹤僅與主要內容相關的時間。 跳過廣告時，不會對本機時間傳回的值執行時間跳變。

   * `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`事件會在即將略過廣告分段之前立即傳送。 您的播放器可以使用此事件來實施與跳過廣告插播相關的自訂邏輯。
   * 退出特技播放會叫用與退出搜尋時相同的廣告播放原則。

      因此，如同在搜尋時，行為取決於應用程式的播放原則是否與預設原則不同。 預設值是最後一個跳過的廣告插播會在您結束竅門遊戲時播放。