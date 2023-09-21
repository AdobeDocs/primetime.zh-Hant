---
description: 您可能需要知道媒體內容為即時或VOD。
title: 識別內容為即時或VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 識別內容為即時或VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容為即時或VOD。

1. 等待瀏覽器TVSDK觸發 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 事件與 `event.status` 之 `AdobePSDK.MediaPlayerStatus.PREPARED`.

   此步驟可確保媒體資源已成功載入。

   >[!IMPORTANT]
   >
   >如果瀏覽器TVSDK未至少在 `PREPARED` 狀態，嘗試呼叫以下方法會擲回 `IllegalStateException`.

1. 讀取 `live` 從 `MediaPlayerItem` 介面：

   ```js
   player.currentItem.live
   ```
