---
description: MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
seo-description: MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。
seo-title: 通知內容
title: 通知內容
uuid: 89fb8f63-b0d5-45cd-bdad-348529fd07d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 通知內容 {#notification-content}

MediaPlayerNotification物件提供播放器狀態、警告和錯誤變更的相關資訊。 停止播放視訊的錯誤也會導致播放器狀態變更。

您的應用程式可以擷取通知和狀態資訊。 您也可以使用通知資訊建立診斷和驗證的記錄系統。

您實作事件監聽器以擷取並回應事件。 許多事件都會提 `MediaPlayerNotification` 供狀態通知。

`MediaPlayerNotification` 提供與播放器狀態相關的資訊。

TVSDK提供通知的時間 `MediaPlayerNotification` 清單。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，例如SEEK_ERROR
   * `metadata`:包含通知相關資訊的金鑰／值配對。 例如，名為的索引鍵 `URL` 提供與通知相關的URL值。

   * `innerNotification`:對其他對象的 `MediaPlayerNotification` 引用直接影響此通知。

您可以將這些資訊儲存在本機以供日後分析，或將它傳送至遠端伺服器以進行記錄和圖形表示。

## 設定通知系統 {#set-up-your-notification-system}

您可以監聽通知，也可以將自己的通知新增至通知歷史記錄。

Primetime Player通知系統的核心是類別， `Notification` 它代表獨立通知。

類別 `NotificationHistory` 提供累積通知的機制。 它會儲存代表通知集合的通知記錄(NotificationHistoryItem)物件。

若要接收通知：

* 監聽通知
* 新增通知至通知歷史記錄

1. 監聽狀態變更。
1. 實作回 `MediaPlayer.PlaybackEventListener.onStateChanged` 呼。
1. TVSDK會傳遞兩個參數至回呼：

   * 新狀態( `MediaPlayer.PlayerState`)
   * 物 `MediaPlayerNotification` 件

## 新增即時記錄與除錯 {#add-real-time-logging-and-debugging}

您可以使用通知在視訊應用程式中實作即時記錄。

通知系統允許您收集日誌和調試資訊以進行診斷和驗證，而不會給系統造成過大壓力。

>[!IMPORTANT]
>
>記錄後端不是生產設定的一部分，因此不預期處理高負載流量。 如果您的實作不需要完全完成，請考慮資料傳輸的效率，以避免系統超載。

以下是如何擷取通知的範例。

1. 為您的視訊應用程式建立以計時器為基礎的執行執行緒，以定期查詢TVSDK通知系統所收集的資料。

1. 如果計時器的間隔過大，而事件清單的大小過小，則通知事件清單將溢出。 若要避免此溢位，請執行下列其中一項作業：

   * 減少驅動線程輪詢新事件的時間間隔。
   * 增加通知清單的大小。

1. 序列化JSON格式的最新通知事件項目，並將這些項目傳送至遠端伺服器以進行後處理。

   然後，遠程伺服器可以即時圖形化地顯示所提供的資料。
1. 若要偵測通知事件的遺失，請尋找事件索引值順序中的空隙。

   每個通知事件都有一個索引值，該索引值會自動由類 `session.NotificationHistory` 增加。

## ID3標籤 {#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 TVSDK會在HLS串流的傳輸串流(TS)區段層級偵測ID3標籤，並派單事件。 應用程式可從標籤擷取資料。

>[!IMPORTANT]
>
>TVSDK可識別音訊(AAC)和視訊(H.264)串流中的ID3中繼資料（2.3.0或2.4.0版），以及任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它會忽略不屬於其中一種識別版本或格式的ID3標籤。 未指定的編碼會視為UTF8。

當TVSDK偵測到ID3中繼資料時，會以下列資料發出通知：

* InfoCode = 303007
* 類型= ID3
* 名稱=不存在
* ID = 0

1. 實作事件偵聽器， `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 並將其註冊到對 `MediaPlayer` 像。

   TVSDK會在偵測到ID3中繼資料時呼叫此接聽程式。

   >[!NOTE]
   >
   >自訂廣告提示會使用相 `onTimedMetadata` 同事件來指出偵測到新標籤。 這不應造成任何混淆，因為會在資訊清單層級偵測到自訂廣告提示，而ID3標籤內嵌在串流中。 如需詳細資訊，請參閱custom-tags-configure。

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
