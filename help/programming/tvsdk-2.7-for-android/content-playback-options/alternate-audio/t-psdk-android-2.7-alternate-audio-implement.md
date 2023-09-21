---
description: 替代音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊串流的視訊。
title: 存取替代音軌
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 存取替代音軌 {#access-alternate-audio-tracks}

替代音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊串流的視訊。

1. 等待 `MediaPlayer` 至少處於 `MediaPlayerStatus.PREPARED` 狀態。
1. 聆聽 `MediaPlayerEvent.STATUS_CHANGED` 具有狀態的事件 `MediaPlayerStatus.PREPARED`.

   此步驟表示音訊曲目的初始清單可供使用。

1. 從取得可用的音軌 `MediaPlayerItem` 執行個體。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （選用）向使用者展示可用的曲目。
1. 將選取的音軌設定在 `MediaPlayerItem` 執行個體。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
