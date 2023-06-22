---
description: 以下範例說明使用者如何選取隱藏式字幕追蹤。
title: 允許使用者變更曲目
exl-id: 103ca0ad-2707-4e4f-87ee-f55041e4527a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# 允許使用者變更曲目{#allow-the-user-to-change-the-track}

以下範例說明使用者如何選取隱藏式字幕追蹤。

1. 若要顯示可用的隱藏式字幕曲目，請使用 `MediaPlayerItem.closedCaptionsTracks` 屬性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 若要設定目前的隱藏式字幕追蹤，請使用 `MediaPlayerItem.selectClosedCaptionsTrack` 方法。
1. 媒體播放器專案準備就緒後，請使用 ` MediaPlayer.  currentItem ` 方法。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
