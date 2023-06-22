---
description: 後期繫結音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊資料流的視訊。
title: 存取替代音軌
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 存取替代音軌{#access-alternate-audio-tracks}

後期繫結音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊資料流的視訊。

1. 等候 `MediaPlayer` 至少處於「已準備」狀態。
1. 接聽這些事件：

   * `MediaPlayerItemEvent.ITEM_CREATED`：音訊曲目的初始清單可供使用。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`：播放期間音訊曲目變更

1. 從取得可用的音軌 `MediaPlayerItem` 執行個體。
1. （選用）向使用者展示可用的曲目。
1. 將選取的音軌設定在 `MediaPlayerItem` 執行個體。
