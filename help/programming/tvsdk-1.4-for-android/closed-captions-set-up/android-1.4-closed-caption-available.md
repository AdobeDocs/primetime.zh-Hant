---
description: 隱藏式字幕會在聲音無法聽到，或檢視者聽力不佳時，將視訊的音訊部分顯示為熒幕上的文字。
title: 從可用曲目中選取目前的註解曲目
exl-id: 75970604-c318-4621-bad3-caab292c8a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 從可用曲目中選取目前的註解曲目{#select-a-current-caption-track-from-among-available-tracks}

您可以從目前可用的隱藏式字幕曲目清單中選取曲目。 這會變成目前軌跡，當可見性開啟時就會顯示。 有些曲目最初可能不可用，因此請聆聽表示有更多曲目可用的事件。

>[!TIP]
>
>隱藏式字幕一律啟用。 所有預設的隱藏式字幕追蹤都會被視為存在。 預設軌道（例如CC1-CC4、CS1-CS6）列舉於 `ClosedCaptionsTrack.DefaultCCTypes`. 當播放開始時，TVSDK會在任何這些管道上尋找活動。 如果找到活動，則會設定 `isActive` 該追蹤的方法，並派送 `MediaPlayer.PlaybackEventListener.onUpdated` 事件。

1. 等候媒體播放器至少處於PREPARED狀態。
1. 接聽這些事件：

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`：可以使用隱藏式字幕曲目的初始清單

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 實作事件的接聽程式，指出有更多可用的追蹤。 當TVSDK傳送事件時，擷取可用磁軌的目前清單。

   每次發生事件時擷取清單，以確保您始終擁有最新的清單。
