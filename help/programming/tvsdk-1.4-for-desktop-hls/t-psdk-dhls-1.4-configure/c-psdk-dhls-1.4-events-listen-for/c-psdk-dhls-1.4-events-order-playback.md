---
description: TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。
title: 播放事件的順序
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# 播放事件的順序{#order-of-playback-events}

TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

下列範例顯示包含播放事件的某些事件的順序。

* 通過`MediaPlayer.replaceCurrentResource`成功載入媒體資源時，事件順序為：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.INITIALIZED`

* 當透過`MediaPlayer.prepareToPlay`準備播放時，事件的順序為：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 是否插入廣告
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.PREPARED`

* 對於即時／線性串流，當播放視窗前進並解決其他機會時，事件順序為：

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 是否插入廣告

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

下列範例顯示事件的典型進展：

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```

