---
description: 延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-description: 延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-title: 存取替代音軌
title: 存取替代音軌
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 存取替代音軌{#access-alternate-audio-tracks}

延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。

1. 等待MediaPlayer至少處於「已準備」狀態。
1. 聽取此事件：

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:音軌的初始清單可供使用。

1. 從例項取得可用的音軌 `MediaPlayerItem` 。

   `mediaPlayerItem.getAudioTracks()` 1. （選擇性）向使用者呈現可用的追蹤。
1. 在例項上設定選取的音軌 `MediaPlayerItem` 。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`