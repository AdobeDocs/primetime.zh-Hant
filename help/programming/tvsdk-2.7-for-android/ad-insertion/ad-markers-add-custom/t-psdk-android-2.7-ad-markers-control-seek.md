---
description: 您可以覆寫TVSDK在使用自訂廣告標籤時如何處理搜尋廣告的預設行為。
seo-description: 您可以覆寫TVSDK在使用自訂廣告標籤時如何處理搜尋廣告的預設行為。
seo-title: 控制搜尋自訂廣告標籤的播放行為
title: 控制搜尋自訂廣告標籤的播放行為
uuid: 248e914e-81b7-4aa5-a4d5-06ca2666e006
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 控制搜尋自訂廣告標籤的播放行為 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以覆寫TVSDK在使用自訂廣告標籤時如何處理搜尋廣告的預設行為。

依預設，當使用者搜尋自訂廣告標籤放置後所產生的廣告區域或過去廣告區域時，TVSDK會跳過廣告。 這可能與標準廣告插播的目前播放行為不同。 您可以設定TVSDK，在使用者搜尋超過一或多個自訂廣告時，將播放頭重新定位至最近略過的自訂廣告的開頭。

1. 打 `CustomRangeMetadata.setAdjustSeekPosition` 電話 `true`。

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 在中 `customRangeMetadata` 使 `MediaPlayerItemConfig`用。

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```

