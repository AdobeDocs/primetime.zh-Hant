---
description: 隱藏式字幕會在聲音無法聽到，或檢視者聽力困難時，將視訊的音訊部分顯示為文字。
title: 從可用曲目中選取目前的標題曲目
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 從可用曲目中選取目前的標題曲目{#select-a-current-caption-track-from-among-available-tracks}

您可以從目前可用的隱藏式字幕曲目清單中選取曲目。 這會成為目前的軌跡，當可見性開啟時就會顯示。 有些曲目一開始可能無法使用，所以請聆聽指出有更多曲目可供使用的事件。

>[!TIP]
>
>隱藏式字幕一律啟用。 所有預設的隱藏式字幕追蹤都會被視為存在。 預設軌道（例如CC1-CC4、CS1-CS6）列舉於 `ClosedCaptionsTrack.DefaultCCTypes`. 當播放開始時，TVSDK會在任何這些管道上尋找活動。 如果找到活動，則會設定 `isActive` 用於該追蹤和分派的方法 `MediaPlayer.PlaybackEventListener.onUpdated` 事件。

1. 等候媒體播放器至少處於「已準備」狀態。
1. 聆聽下列事件：

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`：可以使用隱藏式字幕追蹤的初始清單

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 實作事件監聽器，指出有更多可用的追蹤。 當TVSDK傳送事件時，會擷取目前可用的磁軌清單。

   每次發生事件時擷取清單，以確保您隨時擁有最新清單。
