---
description: TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。
seo-description: TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。
seo-title: QoS事件
title: QoS事件
uuid: e6ba1e9b-435b-480d-bea9-bff41b4e0b21
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# QoS事件{#qos-events}

TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。

下列範例顯示這些事件的典型進展：

```
// For buffering 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_BEGIN, onBufferingBegin); 
private function onBufferingBegin(event:BufferEvent):void { ... } 
 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_END, onBufferingCompleted); 
private function onBufferingCompleted(event:BufferEvent):void { ... } 
 
// For seeking 
mediaPlayer.addEventListener(SeekEvent.SEEK_BEGIN, onSeekBegin); 
private function onSeekBegin(event:SeekEvent):void { ... } 
 
mediaPlayer.addEventListener(SeekEvent.SEEK_COMPLETED, onSeekCompleted); 
private function onSeekCompleted(event:SeekEvent):void { ... } 
 
...  SeekEvent.SEEK_POSITION_ADJUSTED...  //if the desired 
// seek position is modified by the current advertising policies 
```

