---
description: 您可以從目前可用的隱藏字幕音軌清單中選取音軌。 這會變成目前的軌道，當可見性開啟時就會顯示。 某些音軌一開始可能無法使用，因此請監聽表示有更多音軌可供使用的事件。
seo-description: 您可以從目前可用的隱藏字幕音軌清單中選取音軌。 這會變成目前的軌道，當可見性開啟時就會顯示。 某些音軌一開始可能無法使用，因此請監聽表示有更多音軌可供使用的事件。
seo-title: 從可用字軌中選擇目前的字幕軌
title: 從可用字軌中選擇目前的字幕軌
uuid: d582779a-2789-4e2a-85f6-1a0b9b847382
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# 從可用字軌{#select-a-current-caption-track-from-among-available-tracks}中選擇當前字軌

您可以從目前可用的隱藏字幕音軌清單中選取音軌。 這會變成目前的軌道，當可見性開啟時就會顯示。 某些音軌一開始可能無法使用，因此請監聽表示有更多音軌可供使用的事件。

1. 等待媒體播放器至少處於`PREPARED`狀態。
1. 聽聽這些活動：

   * `MediaPlayerEvent.STATUS_CHANGED` 狀態為 `MediaPlayerStatus.INITIALIZED`:隱藏字幕軌道的初始清單可用。

1. 取得目前所有可用隱藏字幕音軌的清單。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 選取可用的追蹤作為目前的追蹤。

   例如：

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 實作事件的監聽器，指出有更多可用的追蹤。 當TVSDK派單事件時，擷取目前可用軌道的清單。

   每次發生事件時擷取清單，以確保您始終擁有最新的清單。