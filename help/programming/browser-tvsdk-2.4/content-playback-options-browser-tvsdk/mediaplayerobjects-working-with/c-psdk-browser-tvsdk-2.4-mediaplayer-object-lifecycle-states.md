---
description: 從建立MediaPlayer例項的那一刻到它終止的那一刻，此例項都會從一個狀態轉換到下一個狀態。
title: MediaPlayer物件的生命週期和狀態
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# MediaPlayer物件的生命週期和狀態{#life-cycle-and-states-of-the-mediaplayer-object}

從建立MediaPlayer例項的那一刻到它終止的那一刻，此例項都會從一個狀態轉換到下一個狀態。

可能的狀態如下：

* **閒置**： `MediaPlayerStatus.IDLE`

* **正在初始化**： `MediaPlayerStatus.INITIALIZING`

* **已初始化**： `MediaPlayerStatus.INITIALIZED`

* **正在準備**： `MediaPlayerStatus.PREPARING`

* **已準備**： `MediaPlayerStatus.PREPARED`

* **正在播放**： `MediaPlayerStatus.PLAYING`

* **已暫停**： `MediaPlayerStatus.PAUSED`

* **搜尋**： `MediaPlayerStatus.SEEKING`

* **完成**： `MediaPlayerStatus.COMPLETE`

* **錯誤**： `MediaPlayerStatus.ERROR`

* **已發行**： `MediaPlayerStatus.RELEASED`

完整的狀態清單定義於 `MediaPlayerStatus`.

瞭解播放器的狀態很有用，因為部分操作只有在播放器處於特定狀態時才被允許。 例如， `play` 當處於IDLE狀態時無法呼叫。 必須在達到PREPARED狀態之後呼叫它。 ERROR狀態也會變更後續發生的情況。

載入及播放媒體資源時，播放器會以下列方式轉換：

1. 初始狀態為「閒置」。
1. 您的應用程式呼叫 `MediaPlayer.replaceCurrentResource`，會將播放器移至INITIALIZING狀態。
1. 如果瀏覽器TVSDK成功載入資源，狀態會變更為INITIALIZED。
1. 您的應用程式呼叫 `MediaPlayer.prepareToPlay`，而狀態會變更為「準備中」。
1. 瀏覽器TVSDK會準備媒體串流，並開始廣告解析和廣告插入（如果已啟用）。

   完成此步驟時，會在時間軸中插入廣告，或廣告程式失敗，且播放器狀態會變更為「已準備」。
1. 當應用程式播放和暫停媒體時，狀態會在「正在播放」和「已暫停」之間移動。

   >[!TIP]
   >
   >播放或暫停時，當您離開播放、關閉裝置或切換應用程式時，狀態會變更為「已暫停」，而資源會釋放。 若要繼續，請還原媒體播放器。

1. 當播放器到達資料流結尾時，狀態會變成「完成」。
1. 當您的應用程式發行媒體播放器時，狀態會變更為「已發行」。
1. 如果處理期間發生錯誤，狀態會變更為ERROR。

以下是MediaPlayer例項生命週期的圖例：

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

您可以使用狀態在程式上向使用者提供意見回饋（例如，在等待下一個狀態變更時執行旋轉器），或在播放媒體時執行下一個步驟，例如在呼叫下一個方法之前等待適當的狀態。

例如：

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```
