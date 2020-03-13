---
description: 以下是使用者如何選擇隱藏字幕軌道的範例。
seo-description: 以下是使用者如何選擇隱藏字幕軌道的範例。
seo-title: 允許使用者變更軌道
title: 允許使用者變更軌道
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 允許使用者變更軌道{#allow-the-user-to-change-the-track}

以下是使用者如何選擇隱藏字幕軌道的範例。

1. 若要顯示可用的隱藏字幕軌道，請使用 `MediaPlayerItem.closedCaptionsTracks` 屬性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 若要設定目前的隱藏字幕軌道，請使用 `MediaPlayerItem.selectClosedCaptionsTrack` 方法。
1. 準備好媒體播放器項目後，使用方法從媒體播放器中檢 ` MediaPlayer.  currentItem ` 索。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

