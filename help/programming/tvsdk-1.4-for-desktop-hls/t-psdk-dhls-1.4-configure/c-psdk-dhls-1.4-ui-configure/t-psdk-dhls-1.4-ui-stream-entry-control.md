---
description: 預設情況下，當開始播放時，VOD媒體從0開始，而即時媒體從客戶端即時點(DefaultMediaPlayer.LIVE_POINT)開始。
title: 在特定時間輸入流
exl-id: b97dbabf-e2ab-4669-a9f3-9129af938a40
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 在特定時間輸入流{#enter-a-stream-at-a-specific-time}

預設情況下，當開始播放時，VOD媒體從0開始，而即時媒體從客戶端即時點(DefaultMediaPlayer.LIVE_POINT)開始。

將位置傳遞到 `MediaPlayer.prepareToPlay`。

TVSDK將給定位置視為資產的起點。 不需要查找操作。 如果位置不在可瀏覽範圍內，則使用預設位置。

例如：

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
