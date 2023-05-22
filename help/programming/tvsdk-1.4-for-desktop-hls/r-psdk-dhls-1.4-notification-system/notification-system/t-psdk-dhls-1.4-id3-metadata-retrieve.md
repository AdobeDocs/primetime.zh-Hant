---
description: ID3標籤提供有關音頻或視頻檔案的資訊，如檔案的標題或藝術家的姓名。 在HLS流中的傳輸流(TS)段級別檢測ID3標籤並調度事件。 應用程式可以從標籤中提取資料。
title: ID3標籤
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# ID3標籤{#id-tags}

ID3標籤提供有關音頻或視頻檔案的資訊，如檔案的標題或藝術家的姓名。 在HLS流中的傳輸流(TS)段級別檢測ID3標籤並調度事件。 應用程式可以從標籤中提取資料。

>[!IMPORTANT]
>
>TVSDK在音頻(AAC)和視頻(H.264)流中識別ID3元資料(2.3.0或2.4.0版)，其任何可能的編碼（ASCII、UTF8、UTF16-BE或UTF16-LE）。 它忽略不在識別的版本或格式之一的ID3標籤。 未指定的編碼被視為UTF8。

當TVSDK檢測到ID3元資料時，它會發出以下資料的通知：

* InfoCode = 303007
* 類型= ID3
* 名稱=不存在
* ID = 0

1. 為實現 `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` 並註冊到 `MediaPlayer` 的雙曲餘切值。

   TVSDK在檢測到ID3元資料時調用此偵聽器。

   >[!NOTE]
   >
   >自定義廣告提示使用相同 `onTimedMetadata` 事件，指示檢測到新標籤。 這不應引起任何混淆，因為在清單級別檢測到自定義廣告提示，並且ID3標籤嵌入到流中。 有關詳細資訊，請參見custom-tags-configure。

1. 檢索元資料。

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
