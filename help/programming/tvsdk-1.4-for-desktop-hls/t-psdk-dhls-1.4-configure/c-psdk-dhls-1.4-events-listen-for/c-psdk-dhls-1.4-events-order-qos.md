---
description: TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝和搜尋事件。
title: QoS事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝和搜尋事件。

下列範例顯示這些事件的典型進度：

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
