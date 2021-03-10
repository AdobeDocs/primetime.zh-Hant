---
title: 視訊播放的基本操作
description: PlaybackManager提供HLS串流的基本操作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 視訊播放的基本操作{#essential-operations-of-video-playback}

PlaybackManager提供HLS串流的基本操作：

* 叫用[PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，以適當回應視訊事件。
* 提供播放操作，例如播放、暫停和搜尋。
* 傳回播放器的相關資訊，例如播放器狀態、播放範圍和視訊即時串流。
* 確定是否啟用了ABR，並根據提供的配置資料設定ABR和緩衝器控制參數。
* 確定是否啟用了緩衝控制，並根據提供的配置資料設定緩衝控制參數。