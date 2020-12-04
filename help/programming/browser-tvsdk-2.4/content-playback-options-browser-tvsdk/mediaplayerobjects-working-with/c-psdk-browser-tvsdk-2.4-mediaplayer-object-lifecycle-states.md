---
description: 從建立MediaPlayer例項到終止該例項的那一刻起，該例項會從一個狀態轉換為下一個狀態。
seo-description: 從建立MediaPlayer例項到終止該例項的那一刻起，該例項會從一個狀態轉換為下一個狀態。
seo-title: MediaPlayer物件的生命週期和狀態
title: MediaPlayer物件的生命週期和狀態
uuid: fe76ea80-aaa8-43bc-9b81-85e0551f70dd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# MediaPlayer物件的生命週期與狀態{#life-cycle-and-states-of-the-mediaplayer-object}

從建立MediaPlayer例項到終止該例項的那一刻起，該例項會從一個狀態轉換為下一個狀態。

以下是可能的狀態：

* **空閒**:  `MediaPlayerStatus.IDLE`

* **初始化**:  `MediaPlayerStatus.INITIALIZING`

* **初始化**:  `MediaPlayerStatus.INITIALIZED`

* **準備**:  `MediaPlayerStatus.PREPARING`

* **準備**:  `MediaPlayerStatus.PREPARED`

* **播放**:  `MediaPlayerStatus.PLAYING`

* **暫停**:  `MediaPlayerStatus.PAUSED`

* **搜尋**:  `MediaPlayerStatus.SEEKING`

* **完成**:  `MediaPlayerStatus.COMPLETE`

* **錯誤**:  `MediaPlayerStatus.ERROR`

* **發行**:  `MediaPlayerStatus.RELEASED`

狀態的完整清單在`MediaPlayerStatus`中定義。

瞭解玩家的狀態很有用，因為有些操作只有在玩家處於特定狀態時才允許。 例如，`play`在IDLE狀態下無法呼叫。 必須在達到準備狀態後呼叫。 ERROR狀態也會更改接下來可能發生的情況。

當載入和播放媒體資源時，播放器會以下列方式轉換：

1. 初始狀態為IDLE。
1. 您的應用程式呼叫`MediaPlayer.replaceCurrentResource`，這會將播放器移至INITIALIZING狀態。
1. 如果瀏覽器TVSDK成功載入資源，狀態會變更為「已初始化」。
1. 您的應用程式呼叫`MediaPlayer.prepareToPlay`，而狀態會變更為「準備」。
1. 瀏覽器TVSDK會準備媒體串流，並啟動廣告解析和廣告插入（如果已啟用）。

   當此步驟完成時，廣告會插入時間軸或廣告程式失敗，而播放器狀態會變更為PREPARED。
1. 當您的應用程式播放和暫停媒體時，狀態會在播放和暫停之間移動。

   >[!TIP]
   >
   >播放或暫停時，當您從播放導覽離開、關閉裝置或切換應用程式時，狀態會變更為「暫停」並釋放資源。 要繼續，請恢復媒體播放器。

1. 當播放器到達串流結尾時，狀態會變為COMPLETE。
1. 當您的應用程式發行媒體播放器時，狀態會變更為「已發行」。
1. 如果在處理過程中發生錯誤，則狀態將更改為ERROR。

以下是MediaPlayer實例生命週期的圖例：

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

您可以使用狀態來提供有關程式的回饋給使用者（例如，等待下一個狀態變更時的微調器），或在播放媒體時採取後續步驟，例如在呼叫下一個方法之前等待適當的狀態。

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

