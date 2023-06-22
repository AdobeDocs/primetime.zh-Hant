---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 TVSDK會在HLS資料流的傳輸資料流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。
title: ID3標籤
exl-id: a0b6ef0b-a8e1-44fa-ab34-3be60a2997c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# ID3標籤 {#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 TVSDK會在HLS資料流的傳輸資料流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。

>[!IMPORTANT]
>
>TVSDK會將ID3中繼資料（2.3.0版或2.4.0版）識別為音訊(AAC)和視訊(H.264)串流，以及其任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它會忽略不具任一認可版本或格式的ID3標籤。 未指定的編碼會視為UTF8。

當TVSDK偵測ID3中繼資料時，會發出包含以下資料的通知：

* 資訊碼= 303007
* 型別= ID3
* 名稱=不存在
* 識別碼= 0

1. 實作事件接聽程式 `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 並向 `MediaPlayer` 物件。

   TVSDK在偵測ID3中繼資料時，會呼叫此監聽器。

   >[!NOTE]
   >
   >自訂廣告提示使用相同的 `onTimedMetadata` 表示偵測到新標籤的事件。 這不會造成任何混淆，因為在資訊清單層級偵測到自訂廣告提示，且ID3標籤內嵌在資料流中。 如需詳細資訊，請參閱自訂標籤設定。

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
