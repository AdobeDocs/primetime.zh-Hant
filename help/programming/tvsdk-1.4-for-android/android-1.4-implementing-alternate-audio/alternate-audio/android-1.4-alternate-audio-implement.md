---
description: 後期綁定音頻使用MediaPlayer播放M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。
title: 訪問備用音頻軌道
exl-id: d357bcc9-2996-42f0-a733-482f59e938ac
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 訪問備用音頻軌道{#access-alternate-audio-tracks}

後期綁定音頻使用MediaPlayer播放M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。

1. 等待MediaPlayer至少處於PREPARED狀態。
1. 收聽此事件：

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:音頻軌道的初始清單可用。

1. 從 `MediaPlayerItem` 實例。

   `mediaPlayerItem.getAudioTracks()` 1. （可選）向用戶顯示可用的軌道。
1. 在 `MediaPlayerItem` 實例。

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
