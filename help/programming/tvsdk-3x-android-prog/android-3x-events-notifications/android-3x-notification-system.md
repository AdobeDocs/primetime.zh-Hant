---
description: 事件和通知可協助您管理視訊應用程式的非同步層面。
title: 播放器狀態、活動、錯誤和記錄的通知和事件
exl-id: 39149c41-920b-4016-9f31-83e772f41cab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 播放器狀態、活動、錯誤和記錄的通知和事件 {#notifications-and-events-for-player-status-activity-errors-and-logging}

事件和通知可協助您管理視訊應用程式的非同步層面。

`MediaPlayerStatus` 物件會提供有關播放器狀態變更的資訊。 `Notification` 物件提供有關警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態的變更。 您可以實作事件接聽程式來擷取和回應事件( `MediaPlayerEvent` 物件)。

您的應用程式可以擷取通知和狀態資訊。 使用此資訊，您也可以建立用於診斷和驗證的記錄系統。

## 通知內容 {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` 提供與播放器狀態相關的資訊。

TVSDK提供以下專案的時間順序清單： `MediaPlayerNotification` 通知，每個通知都包含以下資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`：資訊、警告或錯誤。
   * `code`：通知的數字表示法。
   * `name`：可讀取的通知說明，例如SEEK_ERROR
   * `metadata`：包含通知相關資訊的索引鍵/值組。 例如，名為的金鑰 `URL` 提供一個值，該值為與通知相關的URL。

   * `innerNotification`：對另一個的參照 `MediaPlayerNotification` 直接影響此通知的物件。

您可以將此資訊儲存在本機，供日後分析使用，或傳送至遠端伺服器以供記錄及圖形化顯示。

## 設定您的通知系統 {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

您可以監聽通知。

Primetime播放器通知系統的核心為 `Notification` 類別，代表獨立通知。

若要接收通知，請接聽通知，如下所示：

1. 實作 `NotificationEventListener.onNotification()` callback。
1. TVSDK傳遞 `NotificationEvent` 物件至回呼。

   >[!NOTE]
   >
   >通知型別列於 `Notification.Type` 列舉：

   * `ERROR`
   * `INFO`
   * `WARNING`

## 新增即時記錄與偵錯 {#section_9D4004308CB243AD9B50818895D10005}

您可以使用通知在視訊應用程式中實作即時記錄。

通知系統可讓您收集記錄和偵錯資訊，以進行診斷和驗證，而不需加重系統負擔。

>[!IMPORTANT]
>
>記錄後端不是生產設定的一部分，預期不會處理高負載流量。 如果您的實作不需要完全完成，請考慮資料傳輸的效率，以避免系統過載。

以下是如何擷取通知的範例：

1. 為您的視訊應用程式建立以計時器為基礎的執行執行緒，以定期查詢TVSDK通知系統所收集的資料。
1. 如果計時器的間隔太大，而事件清單太小，則通知事件清單會溢位。

   >[!NOTE]
   >
   >若要避免此溢位，請執行下列任一項作業：
   >
   >1. 縮短驅動輪詢新事件的執行緒的時間間隔。
   >
   >1. 增加通知清單的大小。


1. 以JSON格式序列化最新的通知事件專案，並將這些專案傳送至遠端伺服器以進行後續處理。

   >[!NOTE]
   >
   >遠端伺服器可以圖形化方式即時顯示提供的資料。

1. 若要偵測通知事件遺失，請尋找事件索引值序列中的間隙。
