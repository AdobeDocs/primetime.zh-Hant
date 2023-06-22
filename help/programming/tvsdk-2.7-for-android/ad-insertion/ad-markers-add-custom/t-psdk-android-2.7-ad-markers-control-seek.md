---
description: 使用自訂廣告標籤時，您可以覆寫TVSDK處理方式搜尋廣告的預設行為。
title: 控制搜尋自訂廣告標籤的播放行為
exl-id: 5c17809b-f78b-49f7-85a4-9072502f4a24
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制搜尋自訂廣告標籤的播放行為 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

使用自訂廣告標籤時，您可以覆寫TVSDK處理方式搜尋廣告的預設行為。

根據預設，當使用者搜尋或經過自訂廣告標籤放置造成的廣告區段時，TVSDK會略過廣告。 這可能與標準廣告插播目前的播放行為不同。 您可以設定TVSDK，當使用者搜尋超過一個或多個自訂廣告時，將播放點重新定位到最近略過的自訂廣告的開頭。

1. 呼叫 `CustomRangeMetadata.setAdjustSeekPosition` 替換為 `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 使用 `customRangeMetadata` 在 `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
