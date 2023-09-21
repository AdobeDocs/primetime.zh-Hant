---
description: TVSDK可處理即時視訊串流中的中斷，並在中斷期間提供替代內容。
title: 處理即時資料流中的中斷
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 處理即時資料流中的中斷{#handle-blackouts-in-live-streams}

TVSDK可處理即時視訊串流中的中斷，並在中斷期間提供替代內容。

程式設計中斷最常見的使用案例是播放器應用程式為不符合觀看主流資格的使用者提供替代內容時。 此應用程式可使用TVSDK來判斷中斷期間的開始和結束。 如此一來，在中斷期間開始時，播放可以從中斷期間從主要資料流切換至替代資料流，然後在中斷期間結束後切換回主要資料流。

若要針對此使用案例實作解決方案：

1. 設定您的應用程式以訂閱即時資料流資訊清單中的中斷標籤。

   TVSDK無法直接得知中斷標籤，但可在資訊清單檔案剖析期間遇到特定標籤時，讓應用程式訂閱通知。
1. 新增通知接聽程式 `PTTimedMetadataChangedNotification`.

   每次在資訊清單中剖析訂閱的標籤時，都會傳送此通知，並會傳送新的 `PTTimedMetadata` 已從中準備。

1. 實作監聽器方法，例如 `onMediaPlayerSubscribedTagIdentified`，代表 `PTTimedMetadata` 前景中的物件。

1. 每次在播放期間有更新時，請使用 `PTMediaPlayerTimeChangeNotification` 要處理的監聽器 `PTTimedMetadata` 物件。

1. 新增 `PTTimedMetadata` 處理常式。

   此處理常式可讓您切換至替代內容，並返回主內容，如 `PTTimedMetadata` 物件及其播放時間。

1. 使用 `onSubscribedTagInBackground` 實作監聽器方法 `PTTimedMetadata` 背景中的物件。

   此方法會監控背景資料流上的時間，這有助於您決定何時可以從替代內容切換回主要內容。

1. 針對背景錯誤實作監聽器方法。
1. 如果中斷範圍在播放資料流的DVR中，請更新不可搜尋的範圍。

   在下列情況下，您的應用程式必須在DVR中設定不可搜尋的範圍：

   * 當DVR中出現中斷時加入主串流。
   * 從替代內容切換回主要內容時。
