---
description: 即時啟動會在一或多個通道上預載部分媒體。 當使用者選取或切換頻道後，由於部分緩衝已完成，內容會更早開始。
seo-description: 即時啟動會在一或多個通道上預載部分媒體。 當使用者選取或切換頻道後，由於部分緩衝已完成，內容會更早開始。
seo-title: 立即啟動
title: 立即啟動
uuid: 23864919-9045-4223-9e47-464e38ebe5ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 立即啟動{#instant-on}

即時啟動會在一或多個通道上預載部分媒體。 當使用者選取或切換頻道後，由於部分緩衝已完成，內容會更早開始。

當您的播放器處於狀 `PTMediaPlayerStatusReady` 態時，請呼 `prepareToPlay` 叫以預先載入並處理部分內容，以供稍後播放。

>[!TIP]
>
>如果您未呼叫， `prepareToPlay`呼叫會 `play` 先自動呼 `prepareToPlay` 叫。 此時完成預載和處理。

TVSDK會完成下列部分或全部工作 `prepareToPlay`:

* 若已設定中繼 `kSyncCookiesWithAVAsset` 資料金鑰，TVSDK會向原始M3U8檔案發出一個要求，以同步Cookie。
* 載入DRM中繼資料索引鍵。
* 建立並準備播放內容所需的某些結構、元素或資產。

>[!TIP]
>
>方 `PTMediaPlayer` 法 `PTMediaPlayerItem` 和 `prepareToPlay` 方法相同。 若要避免為每個資 `PTMediaPlayer` 產建立個別例項，請使用 `PTMediaPlayerItem` 方法。

Instant-on可協助您在背景中同時啟動多個媒體播放器例項或媒體播放器項目載入器例項，並在所有這些例項中緩衝視訊串流。 當使用者變更頻道，而串流已正確緩衝時，新頻道上的呼 `play` 叫會提早開始播放。
