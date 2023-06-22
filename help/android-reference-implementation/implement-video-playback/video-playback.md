---
title: 視訊播放的基本作業
description: PlaybackManager提供HLS串流的基本操作
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 視訊播放的基本作業 {#essential-operations-of-video-playback}

PlaybackManager提供HLS串流的基本操作：

* 叫用 [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，可適當回應視訊事件。
* 提供播放、暫停和搜尋等播放作業。
* 傳回播放器的相關資訊，例如播放器狀態、播放範圍和視訊即時資料流。
* 判斷是否已啟用ABR，並根據提供的組態資料設定ABR和緩衝區控制引數。
* 判斷是否已啟用緩衝區控制，並根據提供的組態資料設定緩衝區控制引數。
