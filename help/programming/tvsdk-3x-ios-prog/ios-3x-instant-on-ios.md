---
description: 即時載入在一個或多個頻道上預載部分介質。 在用戶選擇或切換頻道後，內容將更早啟動，因為某些緩衝已完成。
title: 即時
exl-id: 096104a7-867f-43e3-8433-f697d0224e21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 即時 {#instant-on}

即時載入在一個或多個頻道上預載部分介質。 在用戶選擇或切換頻道後，內容將更早啟動，因為某些緩衝已完成。

當你的玩家在 `PTMediaPlayerStatusReady` 狀態，呼叫 `prepareToPlay` 以預載入並處理某些內容，以供以後播放。

>[!TIP]
>
>如果你不打電話 `prepareToPlay`調用 `play` 自動呼叫 `prepareToPlay` 。 預載入和處理在此時完成。

TVSDK完成以下部分或全部任務 `prepareToPlay`:

* 如果元資料鍵 `kSyncCookiesWithAVAsset` 設定後，TVSDK向原始M3U8檔案發出一個請求以同步cookie。
* 載入DRM元資料密鑰。
* 建立和準備播放內容所需的某些結構、元素或資產。

>[!TIP]
>
>的 `PTMediaPlayer` 和 `PTMediaPlayerItem` `prepareToPlay` 方法是相等的。 避免建立單獨 `PTMediaPlayer` 每個資產的實例，使用 `PTMediaPlayerItem` 的雙曲餘切值。

即時啟動可幫助您同時在後台啟動多個媒體播放器實例或媒體播放器項目載入器實例，並在所有這些實例中緩衝視頻流。 當用戶更改頻道，並且流已正確緩衝時，調用 `play` 在新頻道上更早開始播放。
