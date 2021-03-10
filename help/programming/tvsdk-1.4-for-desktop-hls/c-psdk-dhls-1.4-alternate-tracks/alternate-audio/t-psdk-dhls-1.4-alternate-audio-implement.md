---
description: 延遲系結音訊會使用MediaPlayer來播放M3U8 HLS播放清單中指定且可包含數個替代音訊串流的視訊。
title: 存取替代音軌
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
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
