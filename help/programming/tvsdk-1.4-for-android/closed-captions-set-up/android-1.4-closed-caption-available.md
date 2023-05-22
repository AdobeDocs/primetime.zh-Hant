---
description: 當聲音不可聽或觀眾聽不到時，關閉字幕將視頻的音頻部分作為文本顯示在螢幕上。
title: 從可用字幕資訊中選擇當前字幕資訊
exl-id: 75970604-c318-4621-bad3-caab292c8a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 從可用字幕資訊中選擇當前字幕資訊{#select-a-current-caption-track-from-among-available-tracks}

您可以從當前可用的隱藏字幕字幕字幕字幕資訊清單中選擇一個字幕資訊。 這將成為當前軌道，當可見性開啟時顯示。 某些軌道最初可能不可用，因此請偵聽表示更多已可用的事件。

>[!TIP]
>
>始終啟用隱藏字幕。 所有預設的隱藏字幕軌道都被視為存在。 預設磁軌（如CC1-CC4、CS1-CS6）在中枚舉 `ClosedCaptionsTrack.DefaultCCTypes`。 播放開始時，TVSDK會在這些頻道中查找活動。 如果它找到活動，它將 `isActive` 跟蹤和調度的方法 `MediaPlayer.PlaybackEventListener.onUpdated` 的子菜單。

1. 等待媒體播放器至少處於PREPARED狀態。
1. 聽聽這些事件：

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:隱藏字幕軌道的初始清單可用

1. 獲取當前所有可用的隱藏字幕軌道的清單。

   例如：

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
         mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. 選擇可用的跟蹤作為當前跟蹤。

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

1. 為指示有更多磁軌可用的事件實現偵聽器。 當TVSDK派單事件時，檢索當前可用軌道清單。

   每次事件發生時檢索清單，以確保始終擁有最新的清單。
