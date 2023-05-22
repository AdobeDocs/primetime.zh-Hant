---
description: MediaPlayerNotification對象提供有關播放器狀態、警告和錯誤更改的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。
title: 通知內容
exl-id: b8298865-0389-4610-b495-b8735ef9cd56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 通知內容 {#notification-content}

MediaPlayerNotification對象提供有關播放器狀態、警告和錯誤更改的資訊。 停止播放視頻的錯誤還導致播放器的狀態發生更改。

您的應用程式可以檢索通知和狀態資訊。 您還可以使用通知資訊建立診斷和驗證的日誌記錄系統。

實現事件偵聽器以捕獲和響應事件。 許多事件提供 `MediaPlayerNotification` 狀態通知。

`MediaPlayerNotification` 提供與播放器狀態相關的資訊。

TVSDK提供按時間順序排列的 `MediaPlayerNotification` 通知。 每個通知都包含以下資訊：

* 時間戳
* 包含以下元素的診斷元資料：

   * `type`:資訊、警告或錯誤。
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，如SEEK_ERROR
   * `metadata`:包含有關通知的相關資訊的鍵/值對。 例如，名為 `URL` 提供與通知相關的URL的值。

   * `innerNotification`:對另一個的引用 `MediaPlayerNotification` 直接影響此通知的對象。

您可以將此資訊本地儲存以供以後分析，或將其發送到遠程伺服器以進行日誌記錄和圖形表示。

## 設定通知系統 {#set-up-your-notification-system}

您可以監聽通知，也可以將自己的通知添加到通知歷史記錄中。

黃金時段播放器通知系統的核心是 `Notification` 類，表示獨立通知。

的 `NotificationHistory` 類提供了累計通知的機制。 它儲存表示通知集合的通知日誌(NotificationHistoryItem)對象。

要接收通知，請執行以下操作：

* 偵聽通知
* 將通知添加到通知歷史記錄

1. 偵聽狀態更改。
1. 實施 `MediaPlayer.PlaybackEventListener.onStateChanged` 回叫。
1. TVSDK將兩個參數傳遞給回調：

   * 新狀態( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` 對象

## 添加即時日誌記錄和調試 {#add-real-time-logging-and-debugging}

您可以使用通知在視頻應用程式中實現即時記錄。

通知系統允許您收集日誌和調試資訊，以便進行診斷和驗證，而不會過度給系統帶來壓力。

>[!IMPORTANT]
>
>記錄後端不是生產設定的一部分，不應處理高負載流量。 如果您的實施不需要完全完成，請考慮資料傳輸的效率以避免系統過載。

下面是如何檢索通知的示例。

1. 為視頻應用程式建立基於計時器的執行線程，該線程定期查詢TVSDK通知系統收集的資料。

1. 如果計時器的間隔太大，而事件清單的大小太小，則通知事件清單將溢出。 要避免此溢出，請執行以下操作之一：

   * 減少驅動輪詢新事件的線程的時間間隔。
   * 增加通知清單的大小。

1. 以JSON格式序列化最新通知事件項，並將這些項發送到遠程伺服器以進行後處理。

   然後，遠程伺服器可以圖形化地即時顯示所提供的資料。
1. 要檢測通知事件的丟失，請查找事件索引值序列中的間隙。

   每個通知事件都有一個索引值，該索引值由 `session.NotificationHistory` 類。

## ID3標籤 {#id-tags}

ID3標籤提供有關音頻或視頻檔案的資訊，如檔案的標題或藝術家的姓名。 TVSDK檢測HLS流中傳輸流(TS)段級別的ID3標籤並調度事件。 應用程式可以從標籤中提取資料。

>[!IMPORTANT]
>
>TVSDK在音頻(AAC)和視頻(H.264)流中識別ID3元資料(2.3.0或2.4.0版)，其任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它忽略不在識別的版本或格式之一的ID3標籤。 未指定的編碼被視為UTF8。

當TVSDK檢測到ID3元資料時，它會發出以下資料的通知：

* InfoCode = 303007
* 類型= ID3
* 名稱=不存在
* ID = 0

1. 為實現 `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 並註冊到 `MediaPlayer` 的雙曲餘切值。

   TVSDK在檢測到ID3元資料時調用此偵聽器。

   >[!NOTE]
   >
   >自定義廣告提示使用相同 `onTimedMetadata` 事件，指示檢測到新標籤。 這不應引起任何混淆，因為在清單級別檢測到自定義廣告提示，並且ID3標籤嵌入到流中。 有關詳細資訊，請參見custom-tags-configure。

1. 檢索元資料。

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
