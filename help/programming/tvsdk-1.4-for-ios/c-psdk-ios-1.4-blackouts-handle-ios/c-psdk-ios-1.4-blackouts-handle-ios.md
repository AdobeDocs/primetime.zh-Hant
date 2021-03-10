---
description: TVSDK可處理即時視訊串流中的封鎖，並在封鎖期間提供替代內容。
title: 處理即時串流中的封鎖期
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# 處理即時流中的封鎖{#handle-blackouts-in-live-streams}

TVSDK可處理即時視訊串流中的封鎖，並在封鎖期間提供替代內容。

與程式設計封鎖期相關的最常見使用案例，是您的播放器應用程式為無資格觀看主串流的使用者提供替代內容。 此應用程式可使用TVSDK來判斷封鎖期的開始和結束。 這樣，在封鎖期開始時，回放可以從主流切換到備用流，然後在封鎖期結束時切換回主流。

要為此使用案例實施解決方案，請：

1. 設定您的應用程式以訂閱即時串流資訊清單中的封鎖標籤。

   TVSDK並未直接察覺封鎖標籤，但可讓您的應用程式在資訊清單檔案剖析期間遇到特定標籤時訂閱通知。
1. 為`PTTimedMetadataChangedNotification`添加通知偵聽程式。

   每次在清單中解析預訂的標籤並準備新的`PTTimedMetadata`時，都會發送此通知。

1. 對前景中的`PTTimedMetadata`對象實施偵聽器方法，如`onMediaPlayerSubscribedTagIdentified`。

1. 每次播放期間有更新時，請使用`PTMediaPlayerTimeChangeNotification`偵聽器來處理`PTTimedMetadata`物件。

1. 添加`PTTimedMetadata`處理程式。

   此處理常式可讓您切換至替代內容，並返回主要內容，如`PTTimedMetadata`物件及其播放時間所示。

1. 使用`onSubscribedTagInBackground`實現背景中`PTTimedMetadata`對象的監聽器方法。

   此方法會監控背景串流的時間，協助您判斷何時可以從替代內容切換回主要內容。

1. 實作背景錯誤的監聽器方法。
1. 如果封鎖範圍位於播放串流的DVR中，請更新不可看見的範圍。

   在下列情況下，您的應用程式必須在DVR中設定不可檢視的範圍：

   * 在DVR中封鎖期時加入主串流。
   * 從替代內容切換回主要內容時。

