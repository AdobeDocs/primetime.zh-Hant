---
description: 替代音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
title: 存取替代音軌
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 訪問備用音軌{#access-alternate-audio-tracks}

替代音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。

1. 等待`MediaPlayer`至少處於`MediaPlayerStatus.PREPARED`狀態。
1. 監聽狀態為`MediaPlayerStatus.PREPARED`的`MediaPlayerEvent.STATUS_CHANGED`事件。

   此步驟表示音軌的初始清單可供使用。

1. 從`MediaPlayerItem`實例獲取可用的音軌。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （選擇性）向使用者呈現可用的追蹤。
1. 在`MediaPlayerItem`實例上設定選定的音軌。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

