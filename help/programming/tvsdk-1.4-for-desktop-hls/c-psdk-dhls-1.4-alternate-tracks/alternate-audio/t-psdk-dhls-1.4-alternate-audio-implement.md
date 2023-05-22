---
description: 後期綁定音頻使用MediaPlayer播放M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。
title: 訪問備用音頻軌道
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 訪問備用音頻軌道{#access-alternate-audio-tracks}

後期綁定音頻使用MediaPlayer播放M3U8 HLS播放清單中指定的可包含多個備用音頻流的視頻。

1. 等待 `MediaPlayer` 至少處於「已準備」狀態。
1. 聽聽這些事件：

   * `MediaPlayerItemEvent.ITEM_CREATED`:音頻軌道的初始清單可用。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:播放期間音頻軌道更改

1. 從 `MediaPlayerItem` 實例。
1. （可選）向用戶顯示可用的軌道。
1. 在 `MediaPlayerItem` 實例。
