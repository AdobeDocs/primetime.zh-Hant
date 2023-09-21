---
description: MediaPlayerNotification物件提供有關播放器狀態變更、警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態變更。
title: 通知內容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 通知內容 {#notification-content}

MediaPlayerNotification物件提供有關播放器狀態變更、警告和錯誤的資訊。 停止播放視訊的錯誤也會造成播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊，建立用於診斷和驗證的記錄系統。

您可以實作事件接聽程式來擷取和回應事件。 許多事件提供 `MediaPlayerNotification` 狀態通知。

`MediaPlayerNotification` 提供與播放器狀態相關的資訊。

TVSDK提供以下專案的時間順序清單： `MediaPlayerNotification` 通知。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`：資訊、警告或錯誤。
   * `code`：通知的數字表示法。
   * `name`：人類看得懂的通知說明，例如SEEK_ERROR
   * `metadata`：包含通知相關資訊的索引鍵/值組。 例如，名為的索引鍵 `URL` 會提供一個值，該值為與通知相關的URL。

   * `innerNotification`：對另一個的參照 `MediaPlayerNotification` 直接影響此通知的物件。

您可以將此資訊儲存在本機，以供日後分析使用，或傳送至遠端伺服器以供記錄及以圖形方式呈現。

## 設定您的通知系統 {#set-up-your-notification-system}

您可以監聽通知，也可以將您自己的通知新增至通知歷史記錄。

Primetime播放器通知系統的核心為 `Notification` 類別，代表獨立通知。

此 `NotificationHistory` 類別提供了累積通知的機制。 它會儲存代表通知集合的通知(NotificationHistoryItem)物件的記錄。

若要接收通知：

* 接聽通知
* 將通知新增至通知歷史記錄

1. 接聽狀態變更。
1. 實作 `MediaPlayer.PlaybackEventListener.onStateChanged` 回撥。
1. TVSDK會將兩個引數傳遞至回呼：

   * 新狀態( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 物件

## 新增即時記錄和偵錯 {#add-real-time-logging-and-debugging}

您可以使用通知在視訊應用程式中實作即時記錄。

通知系統可讓您收集記錄和偵錯資訊，以進行診斷和驗證，而不會過度強調系統。

>[!IMPORTANT]
>
>記錄後端不屬於生產設定，且預期不會處理高負載流量。 如果您的實作不需要完全完成，請考慮資料傳輸效率，以避免系統超載。

以下是如何擷取通知的範例。

1. 為您的視訊應用程式建立以計時器為基礎的執行執行緒，以定期查詢TVSDK通知系統所收集的資料。

1. 如果計時器的間隔太大，而事件清單的大小太小，則通知事件清單將會溢位。 若要避免此溢位，請執行下列任一項作業：

   * 縮短驅動輪詢新事件的執行緒的時間間隔。
   * 增加通知清單的大小。

1. 序列化JSON格式的最新通知事件專案，並將這些專案傳送至遠端伺服器以供後續處理。

   遠端伺服器可以圖形化方式即時顯示提供的資料。
1. 若要偵測通知事件遺失，請尋找事件索引值順序中的間隙。

   每個通知事件都有一個索引值，此值會自動增加 `session.NotificationHistory` 類別。

## ID3標籤 {#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 TVSDK會在HLS串流中的傳輸串流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。

>[!IMPORTANT]
>
>TVSDK會將ID3中繼資料（2.3.0版或2.4.0版）識別為音訊(AAC)和視訊(H.264)串流，以及其任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它會忽略不包含在其中一個可辨識的版本或格式中的ID3標籤。 未指定的編碼會視為UTF8。

當TVSDK偵測ID3中繼資料時，會發出包含以下資料的通知：

* 資訊代碼= 303007
* 型別= ID3
* 名稱=不存在
* 識別碼= 0

1. 實作事件接聽程式 `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 並向 `MediaPlayer` 物件。

   TVSDK在偵測ID3中繼資料時，會呼叫此監聽器。

   >[!NOTE]
   >
   >自訂廣告提示使用相同的 `onTimedMetadata` 表示偵測到新標籤的事件。 這應該不會造成任何混淆，因為在資訊清單層級偵測到自訂廣告提示，且ID3標籤內嵌在資料流中。 如需詳細資訊，請參閱custom-tags-configure 。

1. 擷取中繼資料。

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
