---
description: 替代音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-description: 替代音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-title: 存取替代音軌
title: 存取替代音軌
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 存取替代音軌 {#access-alternate-audio-tracks}

替代音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。

1. 等待 `MediaPlayer` 至少處於狀 `MediaPlayerStatus.PREPARED` 態。
1. 監聽狀態 `MediaPlayerEvent.STATUS_CHANGED` 為的活動 `MediaPlayerStatus.PREPARED`。

   此步驟表示音軌的初始清單可供使用。

1. 從例項取得可用的音軌 `MediaPlayerItem` 。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （選擇性）向使用者呈現可用的追蹤。
1. 在例項上設定選取的音軌 `MediaPlayerItem` 。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

