---
description: TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝和查找事件。
title: QoS事件
exl-id: 283555cd-9ba9-45e9-a73e-76aba6993e8a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝和查找事件。

以下示例顯示了這些事件的典型進展：

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
