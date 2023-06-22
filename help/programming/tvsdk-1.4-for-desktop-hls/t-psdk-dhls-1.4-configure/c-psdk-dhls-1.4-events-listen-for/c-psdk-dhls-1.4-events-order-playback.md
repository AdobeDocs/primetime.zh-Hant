---
description: TVSDK會以通常預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。
title: 播放事件的順序
exl-id: d03692f6-04b9-4962-92d1-fad671d06665
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 播放事件的順序{#order-of-playback-events}

TVSDK會以通常預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

下列範例顯示包含播放事件之部分事件的順序。

* 透過成功載入媒體資源時 `MediaPlayer.replaceCurrentResource`，事件的順序為：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZED`

* 透過準備播放時 `MediaPlayer.prepareToPlay`，事件的順序為：

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` 如果已插入廣告
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.PREPARED`

* 對於即時/線性串流，在播放期間，隨著播放視窗前進並解決其他機會，事件的順序為：

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
