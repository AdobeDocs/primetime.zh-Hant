---
description: 您可能需要知道媒體內容是即時或VOD。
seo-description: 您可能需要知道媒體內容是即時或VOD。
seo-title: 識別內容是即時或VOD
title: 識別內容是即時或VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 識別內容是即時或VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時或VOD。

1. 等待瀏覽器TVSDK觸發 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 事件， `event.status` 值為 `AdobePSDK.MediaPlayerStatus.PREPARED`。

   此步驟可確保媒體資源已成功載入。

   >[!IMPORTANT]
   >
   >如果瀏覽器TVSDK至少未處於狀態， `PREPARED` 嘗試呼叫下列方法會引發 `IllegalStateException`。

1. 從 `live` 介面 `MediaPlayerItem` 讀取：

   ```js
   player.currentItem.live
   ```

