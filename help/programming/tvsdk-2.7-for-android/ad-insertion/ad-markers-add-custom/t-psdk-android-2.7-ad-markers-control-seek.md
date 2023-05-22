---
description: 使用自定義廣告標籤時，可以覆蓋TVSDK處理如何查找廣告的預設行為。
title: 用於查找自定義廣告標籤的控制回放行為
exl-id: 5c17809b-f78b-49f7-85a4-9072502f4a24
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 用於查找自定義廣告標籤的控制回放行為 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

使用自定義廣告標籤時，可以覆蓋TVSDK處理如何查找廣告的預設行為。

預設情況下，當用戶查找自定義廣告標籤放置後產生的廣告部分或過去的廣告部分時，TVSDK會跳過廣告。 這可能與標準廣告分段的當前播放行為不同。 您可以設定TVSDK將播放頭重新定位到用戶搜索超過一個或多個自定義廣告時最近跳過的自定義廣告的開頭。

1. 呼叫 `CustomRangeMetadata.setAdjustSeekPosition` 與 `true`。

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 使用 `customRangeMetadata` 在 `MediaPlayerItemConfig`。

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
