---
description: 備用音頻使用MediaPlayer播放M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。
title: 訪問備用音頻軌道
exl-id: e5f5b943-4886-4884-80d2-225b5c7e3aed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 訪問備用音頻軌道 {#access-alternate-audio-tracks}

備用音頻使用MediaPlayer播放M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。

1. 等待 `MediaPlayer` 至少在 `MediaPlayerStatus.PREPARED` 狀態。
1. 聽著 `MediaPlayerEvent.STATUS_CHANGED` 狀態為事件 `MediaPlayerStatus.PREPARED`。

   此步驟表示音頻軌道的初始清單可用。

1. 從 `MediaPlayerItem` 實例。

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. （可選）向用戶顯示可用的軌道。
1. 在 `MediaPlayerItem` 實例。

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
