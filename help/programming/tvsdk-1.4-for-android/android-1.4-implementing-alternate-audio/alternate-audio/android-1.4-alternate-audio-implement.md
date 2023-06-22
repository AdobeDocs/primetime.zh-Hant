---
description: 後期繫結音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊資料流的視訊。
title: 存取替代音軌
exl-id: d357bcc9-2996-42f0-a733-482f59e938ac
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 存取替代音軌{#access-alternate-audio-tracks}

後期繫結音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊資料流的視訊。

1. 等待MediaPlayer至少處於PREPARED狀態。
1. 接聽此事件：

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`：音訊曲目的初始清單可供使用。

1. 從取得可用的音軌 `MediaPlayerItem` 執行個體。

   `mediaPlayerItem.getAudioTracks()` 1. （選用）向使用者展示可用的曲目。
1. 將選取的音軌設定在 `MediaPlayerItem` 執行個體。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
