---
description: TVSDK會以一般預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。
title: 播放事件的順序
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 播放事件的順序{#order-of-playback-events}

TVSDK會以一般預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

下列範例顯示包含播放事件之部分事件的順序。

* 當成功載入媒體資源透過 `MediaPlayer.replaceCurrentResource`，事件的順序為：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZED`

* 準備透過播放 `MediaPlayer.prepareToPlay`，事件的順序為：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 如果已插入廣告
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.PREPARED`

* 對於即時/線性串流，在播放視窗前進且其他機會解決時播放期間，事件的順序為：

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` 如果已插入廣告

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

下列範例顯示事件的典型進度：

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
