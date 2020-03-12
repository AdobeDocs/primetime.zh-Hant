---
description: 當聲音聽不見或觀眾聽不到時，隱藏字幕會將視訊的音訊部分顯示為畫面上的文字。
seo-description: 當聲音聽不見或觀眾聽不到時，隱藏字幕會將視訊的音訊部分顯示為畫面上的文字。
seo-title: 從可用字軌中選擇目前的字幕軌
title: 從可用字軌中選擇目前的字幕軌
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 從可用字軌中選擇目前的字幕軌{#select-a-current-caption-track-from-among-available-tracks}

您可以從目前可用的隱藏字幕音軌清單中選取音軌。 這會變成目前的軌道，當可見性開啟時就會顯示。 某些音軌一開始可能無法使用，因此請監聽表示有更多音軌可供使用的事件。

>[!TIP]
>
>隱藏字幕一律啟用。 所有預設的隱藏字幕軌道皆視為存在。 預設音軌（例如CC1-CC4、CS1-CS6）列舉於中 `ClosedCaptionsTrack.DefaultCCTypes`。 當播放開始時，TVSDK會尋找這些頻道上的活動。 如果找到活動，則會設 `isActive` 定該追蹤的方法並調度事 `MediaPlayer.PlaybackEventListener.onUpdated` 件。

1. 等待媒體播放器至少處於「已準備」狀態。
1. 聽聽這些活動：

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:可使用隱藏字幕軌道的初始清單

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
   
<b>mediaPlayer.getCurrentItem()。selectClosedCaptionsTrack(track);</b>selectedClosedCaptionsIndex = i;}}

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

