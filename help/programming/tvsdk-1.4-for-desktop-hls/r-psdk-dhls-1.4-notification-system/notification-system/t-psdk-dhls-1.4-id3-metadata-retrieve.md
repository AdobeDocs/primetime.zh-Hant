---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 在HLS流的傳輸流(TS)段級別檢測ID3標籤並調度事件。 應用程式可從標籤擷取資料。
title: ID3標籤
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# ID3標籤{#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 在HLS流的傳輸流(TS)段級別檢測ID3標籤並調度事件。 應用程式可從標籤擷取資料。

>[!IMPORTANT]
>
>TVSDK可識別音訊(AAC)和視訊(H.264)串流中的ID3中繼資料（2.3.0或2.4.0版），以及任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它會忽略不屬於其中一種識別版本或格式的ID3標籤。 未指定的編碼會視為UTF8。

當TVSDK偵測到ID3中繼資料時，會以下列資料發出通知：

* InfoCode = 303007
* 類型= ID3
* 名稱=不存在
* ID = 0

1. 實作`TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`的事件偵聽器，並將其註冊到`MediaPlayer`對象。

   TVSDK會在偵測到ID3中繼資料時呼叫此接聽程式。

   >[!NOTE]
   >
   >自訂廣告提示使用相同的`onTimedMetadata`事件來指示偵測到新標籤。 這不應造成任何混淆，因為會在資訊清單層級偵測到自訂廣告提示，而ID3標籤內嵌在串流中。 如需詳細資訊，請參閱custom-tags-configure。

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

