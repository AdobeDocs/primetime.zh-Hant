---
description: 依預設，當開始播放時，VOD媒體會從0開始，而即時媒體會從用戶端即時點(DefaultMediaPlayer.LIVE_POINT)開始。
title: 在特定時間輸入串流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# 在特定時間輸入串流{#enter-a-stream-at-a-specific-time}

依預設，當開始播放時，VOD媒體會從0開始，而即時媒體會從用戶端即時點(DefaultMediaPlayer.LIVE_POINT)開始。

將位置傳遞至`MediaPlayer.prepareToPlay`。

TVSDK會將指定位置視為資產的起點。 不需要查找操作。 如果位置不在可查找範圍內，則使用預設位置。

例如：

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
