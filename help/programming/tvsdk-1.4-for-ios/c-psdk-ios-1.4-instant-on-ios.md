---
description: 即時啟動會在一或多個通道上預載部分媒體。 當使用者選取或切換頻道後，由於部分緩衝已完成，內容會更早開始。
title: 立即啟動
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 立即啟動{#instant-on}

即時啟動會在一或多個通道上預載部分媒體。 當使用者選取或切換頻道後，由於部分緩衝已完成，內容會更早開始。

當您的播放器處於`PTMediaPlayerStatusReady`狀態時，請呼叫`prepareToPlay`以預先載入並處理部分內容，以供稍後播放。

>[!TIP]
>
>如果您未呼叫`prepareToPlay`，呼叫`play`會先自動呼叫`prepareToPlay`。 此時完成預載和處理。

TVSDK完成`prepareToPlay`的下列部分或全部工作：

* 若已設定中繼資料金鑰`kSyncCookiesWithAVAsset`,TVSDK會向原始M3U8檔案發出一個要求，以同步Cookie。
* 載入DRM中繼資料索引鍵。
* 建立並準備播放內容所需的某些結構、元素或資產。

>[!TIP]
>
>`PTMediaPlayer`和`PTMediaPlayerItem` `prepareToPlay`方法相等。 若要避免為每個資產建立個別的`PTMediaPlayer`例項，請使用`PTMediaPlayerItem`方法。

Instant-on可協助您在背景中同時啟動多個媒體播放器例項或媒體播放器項目載入器例項，並在所有這些例項中緩衝視訊串流。 當使用者變更頻道，而串流已正確緩衝時，在新頻道上呼叫`play`會提早開始播放。
