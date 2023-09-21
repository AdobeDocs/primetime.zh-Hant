---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 TVSDK會在HLS串流中的傳輸串流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。
title: ID3標籤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# ID3標籤 {#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 TVSDK會在HLS串流中的傳輸串流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。

>[!IMPORTANT]
>
>TVSDK會以其任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）識別音訊(AAC)和視訊(H.264)資料流中的ID3中繼資料（2.3.0版或2.4.0版）。 它會忽略不包含在其中一個可辨識的版本或格式中的ID3標籤。 未指定的編碼會視為UTF8。

當TVSDK偵測ID3中繼資料時，會發出包含以下資料的通知：

* 型別= ID3
* 名稱= ID3

1. 實作事件接聽程式 `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 並向 `MediaPlayer` 物件。

   TVSDK在偵測到時呼叫此監聽器 `ID3` 中繼資料。

   >[!TIP]
   >
   >自訂廣告提示使用相同的 `onTimedMetadata` 表示偵測到新標籤的事件。 這應該不會造成任何混淆，因為在資訊清單層級偵測到自訂廣告提示，且ID3標籤內嵌在資料流中。 如需詳細資訊，請參閱 [自訂標籤](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


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
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```
