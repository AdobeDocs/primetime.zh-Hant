---
description: 您可以從目前可用的隱藏式字幕曲目清單中選取曲目。 這會成為目前的軌跡，當可見性開啟時就會顯示。 有些曲目一開始可能無法使用，所以請聆聽指出有更多曲目可供使用的事件。
title: 從可用曲目中選取目前的標題曲目
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 從可用曲目中選取目前的標題曲目 {#select-a-current-caption-track-from-among-available-tracks}

您可以從目前可用的隱藏式字幕曲目清單中選取曲目。 這會成為目前的軌跡，當可見性開啟時就會顯示。 有些曲目一開始可能無法使用，所以請聆聽指出有更多曲目可供使用的事件。

1. 等候媒體播放器至少在 `PREPARED` 狀態。
1. 聆聽下列事件：

   * `MediaPlayerEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZED`：可以使用隱藏式字幕追蹤的初始清單。

1. 取得所有目前可用的隱藏式字幕曲目的清單。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 選取要做為目前曲目的可用曲目。

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

1. 實作事件監聽器，指出有更多可用的追蹤。 當TVSDK傳送事件時，會擷取目前可用的磁軌清單。

   每次發生事件時擷取清單，以確保您隨時擁有最新清單。
