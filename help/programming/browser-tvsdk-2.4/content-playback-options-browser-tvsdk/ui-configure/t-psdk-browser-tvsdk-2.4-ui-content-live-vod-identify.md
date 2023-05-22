---
description: 您可能需要知道媒體內容是即時的還是視頻點播的。
title: 確定內容是即時還是VOD
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 確定內容是即時還是VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒體內容是即時的還是視頻點播的。

1. 等待瀏覽器TVSDK觸發 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 事件 `event.status` 共 `AdobePSDK.MediaPlayerStatus.PREPARED`。

   此步驟確保媒體資源已成功載入。

   >[!IMPORTANT]
   >
   >如果瀏覽器TVSDK不在 `PREPARED` 狀態，嘗試調用以下方法將引發 `IllegalStateException`。

1. 閱讀 `live` 從 `MediaPlayerItem` 介面：

   ```js
   player.currentItem.live
   ```
