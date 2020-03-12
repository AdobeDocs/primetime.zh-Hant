---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 TVSDK會在HLS串流的傳輸串流(TS)區段層級偵測ID3標籤，並派單事件。 應用程式可從標籤擷取資料。
seo-description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 TVSDK會在HLS串流的傳輸串流(TS)區段層級偵測ID3標籤，並派單事件。 應用程式可從標籤擷取資料。
seo-title: ID3標籤
title: ID3標籤
uuid: 5e5c5f89-7653-47c1-b9c1-6b9b9b1f8d73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# ID3標籤 {#id-tags}

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

