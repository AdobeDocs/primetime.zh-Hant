---
description: 立即開啟會在一或多個通道上預先載入部分媒體。 使用者選取或切換管道後，內容會更早開始，因為部分緩衝已完成。
title: 立即開啟
exl-id: 3a1b2172-8036-40f1-86b6-8304ef771aa9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 立即開啟{#instant-on}

立即開啟會在一或多個通道上預先載入部分媒體。 使用者選取或切換管道後，內容會更早開始，因為部分緩衝已完成。

當您的播放器在 `PTMediaPlayerStatusReady` 狀態，呼叫 `prepareToPlay` 以預先載入及處理部分內容，以供稍後播放。

>[!TIP]
>
>如果您不呼叫 `prepareToPlay`，呼叫 `play` 自動呼叫 `prepareToPlay` 首先。 預先載入與處理在此時完成。

TVSDK會完成下列部分或全部工作 `prepareToPlay`：

* 如果中繼資料索引鍵 `kSyncCookiesWithAVAsset` ，TVSDK會對原始M3U8檔案提出一項要求，以便同步Cookie。
* 載入DRM中繼資料索引鍵。
* 建立並準備播放內容所需的一些結構、元素或資產。

>[!TIP]
>
>此 `PTMediaPlayer` 和 `PTMediaPlayerItem` `prepareToPlay` 方法相同。 避免建立個別的 `PTMediaPlayer` 對每個資產的執行個體，使用 `PTMediaPlayerItem` 方法。

Instant-on可協助您在背景中同時啟動多個媒體播放器例項，或媒體播放器專案載入器例項，並在所有這些例項中緩衝視訊資料流。 當使用者變更頻道，並且資料流已正確緩衝時，呼叫 `play` 會在新頻道上更早開始播放。
