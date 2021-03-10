---
description: 以下是使用者如何選擇隱藏字幕軌道的範例。
title: 允許使用者變更軌道
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---


# 允許使用者變更track{#allow-the-user-to-change-the-track}

以下是使用者如何選擇隱藏字幕軌道的範例。

1. 若要顯示可用的隱藏字幕軌道，請使用`MediaPlayerItem.closedCaptionsTracks`屬性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 若要設定目前的隱藏字幕軌道，請使用`MediaPlayerItem.selectClosedCaptionsTrack`方法。
1. 準備好媒體播放器項目後，使用` MediaPlayer.  currentItem `方法從媒體播放器中擷取它。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

