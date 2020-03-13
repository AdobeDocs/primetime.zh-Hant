---
seo-title: 視訊播放的基本操作
title: 視訊播放的基本操作
description: PlaybackManager提供HLS串流的基本操作
seo-description: PlaybackManager提供HLS串流的基本操作
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 視訊播放的基本操作 {#essential-operations-of-video-playback}

PlaybackManager提供HLS串流的基本操作：

* 叫用 [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，可適當回應視訊事件。
* 提供播放操作，例如播放、暫停和搜尋。
* 傳回播放器的相關資訊，例如播放器狀態、播放範圍和視訊即時串流。
* 確定是否啟用了ABR，並根據提供的配置資料設定ABR和緩衝器控制參數。
* 確定是否啟用了緩衝控制，並根據提供的配置資料設定緩衝控制參數。