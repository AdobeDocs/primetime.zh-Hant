---
description: 後期繫結音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊資料流的視訊。
title: 存取替代音軌
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 存取替代音軌{#access-alternate-audio-tracks}

後期繫結音訊使用MediaPlayer來播放在M3U8 HLS播放清單中指定，並且可以包含數個替代音訊資料流的視訊。

1. 等待 `MediaPlayer` 至少處於「已準備」狀態。
1. 聆聽下列事件：

   * `MediaPlayerItemEvent.ITEM_CREATED`：可使用音訊曲目的初始清單。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`：播放期間音訊曲目有所變更

1. 從取得可用的音軌 `MediaPlayerItem` 執行個體。
1. （選用）向使用者展示可用的曲目。
1. 將選取的音軌設定在 `MediaPlayerItem` 執行個體。
