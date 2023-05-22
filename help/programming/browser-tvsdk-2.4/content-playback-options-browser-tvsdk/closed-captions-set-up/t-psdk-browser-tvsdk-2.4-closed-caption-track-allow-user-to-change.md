---
description: 下面是用戶如何選擇隱藏字幕軌道的示例。
title: 允許用戶更改軌道
exl-id: 103ca0ad-2707-4e4f-87ee-f55041e4527a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# 允許用戶更改軌道{#allow-the-user-to-change-the-track}

下面是用戶如何選擇隱藏字幕軌道的示例。

1. 要顯示可用的隱藏字幕軌道，請使用 `MediaPlayerItem.closedCaptionsTracks` 屬性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 要設定當前的隱藏字幕軌道，請使用 `MediaPlayerItem.selectClosedCaptionsTrack` 的雙曲餘切值。
1. 在準備媒體播放器項目後，使用 ` MediaPlayer.  currentItem ` 的雙曲餘切值。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
