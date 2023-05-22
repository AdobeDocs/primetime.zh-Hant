---
description: TVSDK處理即時視頻流中的封鎖，並在封鎖期間提供備用內容。
title: 處理封鎖
exl-id: 4a2ff371-69a9-4c13-ac61-3c5cd9c83a6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 處理封鎖 {#handle-blackouts}

TVSDK處理即時視頻流中的封鎖，並在封鎖期間提供備用內容。

與寫程式封鎖相關的最常見使用案例是，您的播放器應用程式向不有資格觀看主流的用戶提供替代內容。 此應用可以使用TVSDK確定封鎖期的開始和結束。 這樣，在封鎖期開始時，回放可以從主流切換到備用流，然後在封鎖期結束時切換回主流。

要實施此用例的解決方案，請執行以下操作：

1. 設定應用以訂閱即時流清單中的封鎖標籤。

   TVSDK不直接知道封鎖標籤，但它允許您的應用在清單檔案分析期間遇到特定標籤時訂閱通知。
1. 添加通知偵聽器 `PTTimedMetadataChangedNotification`。

   每次在清單中分析預訂的標籤時都會調度此通知，並且 `PTTimedMetadata` 是準備好的。

1. 實現監聽器方法，如 `onMediaPlayerSubscribedTagIdentified`, `PTTimedMetadata` 前景中的對象。

1. 每次在播放期間進行更新時，使用 `PTMediaPlayerTimeChangeNotification` 偵聽程式 `PTTimedMetadata` 對象。

1. 添加 `PTTimedMetadata` 處理程式。

   此處理程式允許您切換到備用內容並返回主內容，如 `PTTimedMetadata` 對象及其播放時間。

1. 使用 `onSubscribedTagInBackground` 實現的監聽器方法 `PTTimedMetadata` 對象。

   此方法監視後台流上的計時，這有助於確定何時可以從備用內容切換回主內容。

1. 實現後台錯誤的偵聽器方法。
1. 如果封鎖範圍在播放流的DVR中，請更新不可查找的範圍。

   在以下情況下，您的應用程式必須在DVR中設定不可查的範圍：

   * 在DVR中斷時加入主流時。
   * 從備用內容切換回主內容時。
