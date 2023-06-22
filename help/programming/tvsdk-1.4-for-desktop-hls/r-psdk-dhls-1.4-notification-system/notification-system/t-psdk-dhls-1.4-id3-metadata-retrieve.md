---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 會偵測HLS資料流中傳輸資料流(TS)區段層級的ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。
title: ID3標籤
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# ID3標籤{#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 會偵測HLS資料流中傳輸資料流(TS)區段層級的ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。

>[!IMPORTANT]
>
>TVSDK會將ID3中繼資料（2.3.0版或2.4.0版）識別為音訊(AAC)和視訊(H.264)串流，以及其任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它會忽略不具任一認可版本或格式的ID3標籤。 未指定的編碼會視為UTF8。

當TVSDK偵測ID3中繼資料時，會發出包含以下資料的通知：

* 資訊碼= 303007
* 型別= ID3
* 名稱=不存在
* 識別碼= 0

1. 實作事件接聽程式 `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` 並向 `MediaPlayer` 物件。

   TVSDK在偵測ID3中繼資料時，會呼叫此監聽器。

   >[!NOTE]
   >
   >自訂廣告提示使用相同的 `onTimedMetadata` 表示偵測到新標籤的事件。 這不會造成任何混淆，因為在資訊清單層級偵測到自訂廣告提示，且ID3標籤內嵌在資料流中。 如需詳細資訊，請參閱自訂標籤設定。

1. 擷取中繼資料。

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```
