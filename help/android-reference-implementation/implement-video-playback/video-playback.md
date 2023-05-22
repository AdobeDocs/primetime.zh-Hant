---
title: 視頻播放的基本操作
description: PlaybackManager提供HLS流的基本操作
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 視頻播放的基本操作 {#essential-operations-of-video-playback}

PlaybackManager提供了HLS流的基本操作：

* 調用 [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)，可以對視頻事件做出適當的響應。
* 提供播放操作，如播放、暫停和查找。
* 返回有關播放器的資訊，如播放器狀態、播放範圍和視頻即時流。
* 確定是否啟用ABR，並根據提供的配置資料設定ABR和緩衝區控制參數。
* 確定是否啟用緩衝區控制，並根據提供的配置資料設定緩衝區控制參數。
