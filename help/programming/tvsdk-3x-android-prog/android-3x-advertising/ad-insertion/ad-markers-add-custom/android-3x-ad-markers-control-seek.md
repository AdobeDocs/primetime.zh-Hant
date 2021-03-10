---
description: 您可以覆寫TVSDK在使用自訂廣告標籤時如何處理搜尋廣告的預設行為。
title: 控制搜尋自訂廣告標籤的播放行為
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 控制搜尋自訂廣告標籤{#control-playback-behavior-for-seeking-over-custom-ad-markers}的播放行為

您可以覆寫TVSDK在使用自訂廣告標籤時如何處理搜尋廣告的預設行為。

依預設，當使用者搜尋自訂廣告標籤放置後所產生的廣告區域或過去廣告區域時，TVSDK會跳過廣告。 這可能與標準廣告插播的目前播放行為不同。 您可以設定TVSDK，在使用者搜尋超過一或多個自訂廣告時，將播放頭重新定位至最近略過的自訂廣告的開頭。

1. 使用`true`呼叫`CustomRangeMetadata.setAdjustSeekPosition`。

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 在`MediaPlayerItemConfig`中使用`customRangeMetadata`。

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
