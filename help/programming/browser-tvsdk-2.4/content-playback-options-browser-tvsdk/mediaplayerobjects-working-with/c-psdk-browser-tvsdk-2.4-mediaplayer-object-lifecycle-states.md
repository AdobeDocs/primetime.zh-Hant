---
description: 從建立MediaPlayer實例到終止實例，該實例將從一個狀態轉換到下一個狀態。
title: MediaPlayer對象的生命週期和狀態
exl-id: 26cad982-ef85-42fb-aaa7-e5d494088766
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# MediaPlayer對象的生命週期和狀態{#life-cycle-and-states-of-the-mediaplayer-object}

從建立MediaPlayer實例到終止實例，該實例將從一個狀態轉換到下一個狀態。

以下是可能的狀態：

* **空閒**: `MediaPlayerStatus.IDLE`

* **初始化**: `MediaPlayerStatus.INITIALIZING`

* **已初始化**: `MediaPlayerStatus.INITIALIZED`

* **準備**: `MediaPlayerStatus.PREPARING`

* **準備**: `MediaPlayerStatus.PREPARED`

* **播放**: `MediaPlayerStatus.PLAYING`

* **已暫停**: `MediaPlayerStatus.PAUSED`

* **尋找**: `MediaPlayerStatus.SEEKING`

* **完成**: `MediaPlayerStatus.COMPLETE`

* **錯誤**: `MediaPlayerStatus.ERROR`

* **已發佈**: `MediaPlayerStatus.RELEASED`

狀態的完整清單定義於 `MediaPlayerStatus`。

瞭解玩家的狀態是有用的，因為只有當玩家處於特定狀態時才允許某些操作。 比如說， `play` 在IDLE狀態下無法調用。 必須在達到PREPARED狀態後調用。 ERROR狀態還會更改接下來可能發生的情況。

當媒體資源被載入和播放時，播放器將以下方式轉換：

1. 初始狀態為IDLE。
1. 您的應用程式調用 `MediaPlayer.replaceCurrentResource`，將播放器移動到INITIALIZING狀態。
1. 如果瀏覽器TVSDK成功載入資源，則狀態將更改為INITIALIZED。
1. 您的應用程式調用 `MediaPlayer.prepareToPlay`，並且狀態將更改為PREPARING。
1. 瀏覽器TVSDK準備媒體流並啟動廣告解析和廣告插入（如果啟用）。

   完成此步驟後，廣告將插入時間軸或廣告過程失敗，並且播放器狀態將更改為PREPARED。
1. 當應用程式播放和暫停媒體時，狀態在播放和暫停之間移動。

   >[!TIP]
   >
   >在播放或暫停時，當您從播放中導航、關閉設備或切換應用程式時，狀態將更改為「已掛起」並釋放資源。 要繼續，請恢復媒體播放器。

1. 當播放器到達流的末尾時，狀態變為「完成」。
1. 當應用程式釋放媒體播放器時，狀態將更改為「已釋放」。
1. 如果在處理過程中發生錯誤，則狀態將更改為ERROR。

下面是MediaPlayer實例生命週期的圖示：

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

您可以使用狀態向用戶提供有關該進程的反饋（例如，在等待下一個狀態更改時使用旋轉器），或在播放媒體時採取下一步，例如在調用下一個方法之前等待適當的狀態。

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
