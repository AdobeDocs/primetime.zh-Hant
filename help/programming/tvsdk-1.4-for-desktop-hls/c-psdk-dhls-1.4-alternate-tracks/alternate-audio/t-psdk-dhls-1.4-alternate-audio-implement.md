---
description: 延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-description: 延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
seo-title: 存取替代音軌
title: 存取替代音軌
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# 存取替代音軌{#access-alternate-audio-tracks}

延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。

1. 等待`MediaPlayer`至少處於「已準備」狀態。
1. 聽聽這些活動：

   * `MediaPlayerItemEvent.ITEM_CREATED`:音軌的初始清單可供使用。
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:播放期間音軌已變更

1. 從`MediaPlayerItem`實例獲取可用的音軌。
1. （選擇性）向使用者呈現可用的追蹤。
1. 在`MediaPlayerItem`實例上設定選定的音軌。
