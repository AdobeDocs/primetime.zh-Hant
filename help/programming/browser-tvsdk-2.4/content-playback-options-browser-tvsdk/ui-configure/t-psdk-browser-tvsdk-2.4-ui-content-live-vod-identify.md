---
description: 您可能需要知道媒體內容是即時或VOD。
title: 識別內容是即時或VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# 識別內容是即時或VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時或VOD。

1. 等待瀏覽器TVSDK觸發`AdobePSDK.PSDKEventType.STATUS_CHANGED`事件，其中`event.status`為`AdobePSDK.MediaPlayerStatus.PREPARED`。

   此步驟可確保媒體資源已成功載入。

   >[!IMPORTANT]
   >
   >如果瀏覽器TVSDK至少不處於`PREPARED`狀態，嘗試呼叫下列方法會引發`IllegalStateException`。

1. 從`MediaPlayerItem`介面讀取`live`:

   ```js
   player.currentItem.live
   ```

