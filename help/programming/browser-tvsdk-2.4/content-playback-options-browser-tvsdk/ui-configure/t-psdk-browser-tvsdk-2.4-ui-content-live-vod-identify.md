---
description: 您可能需要知道媒體內容是即時或VOD。
seo-description: 您可能需要知道媒體內容是即時或VOD。
seo-title: 識別內容是即時或VOD
title: 識別內容是即時或VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '106'
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

