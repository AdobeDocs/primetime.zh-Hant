---
description: 事件和通知可幫助您管理視頻應用程式的非同步方面。
title: 播放器狀態、活動、錯誤和記錄的通知和事件
exl-id: 39149c41-920b-4016-9f31-83e772f41cab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 播放器狀態、活動、錯誤和記錄的通知和事件 {#notifications-and-events-for-player-status-activity-errors-and-logging}

事件和通知可幫助您管理視頻應用程式的非同步方面。

`MediaPlayerStatus` 對象提供有關播放器狀態更改的資訊。 `Notification` 對象提供有關警告和錯誤的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。 實現事件偵聽器以捕獲和響應事件( `MediaPlayerEvent` 對象)。

您的應用程式可以檢索通知和狀態資訊。 使用此資訊，您還可以建立日誌系統以進行診斷和驗證。

## 通知內容 {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` 提供與播放器狀態相關的資訊。

TVSDK提供按時間順序排列的 `MediaPlayerNotification` 通知，並且每個通知都包含以下資訊：

* 時間戳
* 包含以下元素的診斷元資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，如SEEK_ERROR
   * `metadata`:包含有關通知的相關資訊的鍵/值對。 例如，名為 `URL` 提供與通知相關的URL的值。

   * `innerNotification`:對另一個的引用 `MediaPlayerNotification` 直接影響此通知的對象。

您可以將此資訊本地儲存以供以後分析，或將其發送到遠程伺服器以進行日誌記錄和圖形表示。

## 設定通知系統 {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

您可以監聽通知。

黃金時段播放器通知系統的核心是 `Notification` 類，表示獨立通知。

要接收通知，請按如下方式偵聽通知：

1. 實施 `NotificationEventListener.onNotification()` 回叫。
1. TVSDK通過 `NotificationEvent` 對象。

   >[!NOTE]
   >
   >在中枚舉通知類型 `Notification.Type` 枚舉：

   * `ERROR`
   * `INFO`
   * `WARNING`

## 添加即時日誌記錄和調試 {#section_9D4004308CB243AD9B50818895D10005}

您可以使用通知在視頻應用程式中實現即時記錄。

通知系統允許您收集日誌和調試資訊以進行診斷和驗證，而不會給系統帶來壓力。

>[!IMPORTANT]
>
>記錄後端不是生產設定的一部分，不應處理高負載流量。 如果您的實施不需要完全完成，請考慮資料傳輸的效率以避免系統過載。

以下是如何檢索通知的示例：

1. 為視頻應用程式建立基於計時器的執行線程，該線程定期查詢TVSDK通知系統收集的資料。
1. 如果計時器的間隔太大，而事件清單的大小太小，則通知事件清單將溢出。

   >[!NOTE]
   >
   >要避免此溢出，請執行以下操作之一：
   >
   >1. 減少驅動輪詢新事件的線程的時間間隔。
   >
   >1. 增加通知清單的大小。


1. 以JSON格式序列化最新通知事件項，並將這些項發送到遠程伺服器以進行後處理。

   >[!NOTE]
   >
   >遠程伺服器可以圖形化地即時顯示所提供的資料。

1. 要檢測通知事件的丟失，請查找事件索引值序列中的間隙。
