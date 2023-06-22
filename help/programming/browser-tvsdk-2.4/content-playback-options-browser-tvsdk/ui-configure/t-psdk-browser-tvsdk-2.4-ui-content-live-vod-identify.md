---
description: 您可能需要知道媒體內容為即時或VOD。
title: 識別內容為即時或VOD
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 識別內容為即時或VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容為即時或VOD。

1. 等候瀏覽器TVSDK觸發 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 具有的事件 `event.status` 之 `AdobePSDK.MediaPlayerStatus.PREPARED`.

   此步驟可確保媒體資源已成功載入。

   >[!IMPORTANT]
   >
   >如果瀏覽器TVSDK未至少位於 `PREPARED` state，嘗試呼叫以下方法會擲回 `IllegalStateException`.

1. 讀取 `live` 從 `MediaPlayerItem` 介面：

   ```js
   player.currentItem.live
   ```
