---
description: 您可以從目前可用的隱藏式字幕曲目清單中選取曲目。 這會變成目前軌跡，當可見性開啟時就會顯示。 有些曲目最初可能不可用，因此請聆聽表示有更多曲目可用的事件。
title: 從可用曲目中選取目前的註解曲目
exl-id: d604dedc-f3c3-4c97-9b0f-84da326c0678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 從可用曲目中選取目前的註解曲目 {#select-a-current-caption-track-from-among-available-tracks}

您可以從目前可用的隱藏式字幕曲目清單中選取曲目。 這會變成目前軌跡，當可見性開啟時就會顯示。 有些曲目最初可能不可用，因此請聆聽表示有更多曲目可用的事件。

1. 等候媒體播放器至少在 `PREPARED` 狀態。
1. 接聽這些事件：

   * `MediaPlayerEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZED`：可以使用隱藏式字幕曲目的初始清單。

1. 取得所有目前可用的隱藏式字幕曲目的清單。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 選取可用曲目作為目前曲目。

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

1. 實作事件的接聽程式，指出有更多可用的追蹤。 當TVSDK傳送事件時，擷取可用磁軌的目前清單。

   每次發生事件時擷取清單，以確保您始終擁有最新的清單。
