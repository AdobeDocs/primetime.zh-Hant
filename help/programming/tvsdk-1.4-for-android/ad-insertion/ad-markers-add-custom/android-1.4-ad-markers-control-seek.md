---
description: 使用自定義廣告標籤時，可以覆蓋TVSDK查找廣告的預設行為。
title: 用於查找自定義廣告標籤的控制回放行為
exl-id: 83faa5a4-4416-499e-8cf2-d016cd9a379d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 用於查找自定義廣告標籤的控制回放行為{#control-playback-behavior-for-seeking-over-custom-ad-markers}

使用自定義廣告標籤時，可以覆蓋TVSDK查找廣告的預設行為。

預設情況下，當用戶查找自定義廣告標籤放置後產生的廣告部分或過去的廣告部分時，TVSDK會跳過廣告。 這可能與標準廣告分段的當前播放行為不同。

當用戶尋找超過一個或多個自定義廣告時，您可以告訴TVSDK將播放頭重新定位到最近跳過的自定義廣告的開頭。

1. 使用 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 枚舉設定為字串值「true」（不是布爾值） `true`)。

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. 建立和配置 `MediaResource` 實例，將附加配置選項傳遞給 `TimeRangeCollection.toMetadata`。 此方法通過另一個通用元資料結構接收附加配置選項。

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```
