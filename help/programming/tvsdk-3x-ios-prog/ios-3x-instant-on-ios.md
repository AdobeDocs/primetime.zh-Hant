---
description: 立即開啟會在一或多個通道上預先載入部分媒體。 使用者選取或切換頻道後，內容會更早開始，因為部分緩衝已完成。
title: 即時開啟
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 即時開啟 {#instant-on}

立即開啟會在一或多個通道上預先載入部分媒體。 使用者選取或切換頻道後，內容會更早開始，因為部分緩衝已完成。

當您的播放器在 `PTMediaPlayerStatusReady` 狀態，呼叫 `prepareToPlay` 以預先載入及處理部分內容，以供稍後播放。

>[!TIP]
>
>如果您不呼叫 `prepareToPlay`，呼叫 `play` 自動呼叫 `prepareToPlay` 第一。 預先載入及處理作業目前已完成。

TVSDK會完成下列部分或全部工作 `prepareToPlay`：

* 如果中繼資料索引鍵 `kSyncCookiesWithAVAsset` 設定，TVSDK會對原始M3U8檔案提出一項要求，以便同步Cookie。
* 載入DRM中繼資料索引鍵。
* 建立並準備播放內容所需的一些結構、元素或資產。

>[!TIP]
>
>此 `PTMediaPlayer` 和 `PTMediaPlayerItem` `prepareToPlay` 方法相同。 若要避免建立個別的 `PTMediaPlayer` 對於每個資產的例項，請使用 `PTMediaPlayerItem` 方法。

Instant-on可協助您在背景同時啟動多個媒體播放器例項，或是在所有這些例項中緩衝視訊資料流。 當使用者變更頻道，並且資料流已正確緩衝時，呼叫 `play` 會在新頻道上更早開始播放。
