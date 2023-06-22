---
description: 使用自訂廣告標籤時，您可以覆寫TVSDK搜尋廣告的預設行為。
title: 控制搜尋自訂廣告標籤的播放行為
exl-id: 83faa5a4-4416-499e-8cf2-d016cd9a379d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 控制搜尋自訂廣告標籤的播放行為{#control-playback-behavior-for-seeking-over-custom-ad-markers}

使用自訂廣告標籤時，您可以覆寫TVSDK搜尋廣告的預設行為。

根據預設，當使用者搜尋或經過自訂廣告標籤放置造成的廣告區段時，TVSDK會略過廣告。 這可能與標準廣告插播目前的播放行為不同。

當使用者搜尋超過一個或多個自訂廣告時，您可以指示TVSDK將播放點重新定位到最近略過的自訂廣告的開頭。

1. 使用設定中繼資料例項 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 列舉設定為字串值「true」（不是布林值） `true`)。

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. 建立及設定 `MediaResource` 執行個體，將其他設定選項傳遞至 `TimeRangeCollection.toMetadata`. 此方法會透過其他一般中繼資料結構接收其他設定選項。

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```
