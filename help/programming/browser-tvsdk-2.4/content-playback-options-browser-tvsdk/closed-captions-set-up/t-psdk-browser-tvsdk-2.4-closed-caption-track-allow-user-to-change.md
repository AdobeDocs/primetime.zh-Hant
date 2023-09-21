---
description: 以下範例說明使用者如何選取隱藏式字幕追蹤。
title: 允許使用者變更追蹤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# 允許使用者變更追蹤{#allow-the-user-to-change-the-track}

以下範例說明使用者如何選取隱藏式字幕追蹤。

1. 若要顯示可用的隱藏式字幕追蹤，請使用 `MediaPlayerItem.closedCaptionsTracks` 屬性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 若要設定目前的隱藏式字幕追蹤，請使用 `MediaPlayerItem.selectClosedCaptionsTrack` 方法。
1. 在媒體播放器專案準備就緒後，請使用 ` MediaPlayer.  currentItem ` 方法。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
