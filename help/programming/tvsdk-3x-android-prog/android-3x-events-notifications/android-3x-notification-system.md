---
description: 事件和通知可協助您管理視訊應用程式的非同步層面。
title: 播放器狀態、活動、錯誤和記錄的通知和事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# 播放器狀態、活動、錯誤和記錄的通知和事件{#notifications-and-events-for-player-status-activity-errors-and-logging}

事件和通知可協助您管理視訊應用程式的非同步層面。

`MediaPlayerStatus` 物件提供播放器狀態變更的相關資訊。`Notification` 對象提供有關警告和錯誤的資訊。停止播放視訊的錯誤也會導致播放器狀態變更。 您實作事件監聽器以擷取並回應事件（`MediaPlayerEvent`物件）。

您的應用程式可以擷取通知和狀態資訊。 使用此資訊，您還可以建立診斷和驗證的日誌記錄系統。

## 通知內容{#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` 提供與播放器狀態相關的資訊。

TVSDK提供`MediaPlayerNotification`通知的時間清單，而每則通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，例如SEEK_ERROR
   * `metadata`:包含通知相關資訊的金鑰／值配對。例如，名為`URL`的索引鍵提供與通知相關的URL值。

   * `innerNotification`:直接影響此通 `MediaPlayerNotification` 知的對其它對象的引用。

您可以將這些資訊儲存在本機以供日後分析，或將它傳送至遠端伺服器以進行記錄和圖形表示。

## 設定通知系統{#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

您可以監聽通知。

Primetime Player通知系統的核心是`Notification`類別，代表獨立通知。

要接收通知，請按如下方式監聽通知：

1. 實作`NotificationEventListener.onNotification()`回呼。
1. TVSDK會將`NotificationEvent`物件傳遞至回呼。

   >[!NOTE]
   >
   >通知類型列舉於`Notification.Type`列舉中：

   * `ERROR`
   * `INFO`
   * `WARNING`

## 新增即時記錄與除錯{#section_9D4004308CB243AD9B50818895D10005}

您可以使用通知在視訊應用程式中實作即時記錄。

通知系統允許您收集日誌和調試資訊以進行診斷和驗證，而不給系統帶來壓力。

>[!IMPORTANT]
>
>記錄後端不是生產設定的一部分，因此不預期處理高負載流量。 如果您的實作不需要完全完成，請考慮資料傳輸的效率，以避免系統超載。

以下是如何擷取通知的範例：

1. 為您的視訊應用程式建立以計時器為基礎的執行執行緒，以定期查詢TVSDK通知系統所收集的資料。
1. 如果計時器的間隔過大，而事件清單的大小過小，則通知事件清單將溢出。

   >[!NOTE]
   >
   >若要避免此溢位，請執行下列其中一項作業：
   >
   >1. 減少驅動線程輪詢新事件的時間間隔。
      >
      >
   1. 增加通知清單的大小。


1. 序列化JSON格式的最新通知事件項目，並將這些項目傳送至遠端伺服器以進行後處理。

   >[!NOTE]
   >
   >遠程伺服器可以即時圖形化地顯示提供的資料。

1. 若要偵測通知事件的遺失，請尋找事件索引值順序中的空隙。