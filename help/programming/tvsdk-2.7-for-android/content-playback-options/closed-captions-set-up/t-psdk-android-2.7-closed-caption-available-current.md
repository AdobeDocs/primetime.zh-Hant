---
description: 您可以從當前可用的隱藏字幕字幕字幕字幕資訊清單中選擇一個字幕資訊。 這將成為當前軌道，當可見性開啟時顯示。 某些軌道最初可能不可用，因此請偵聽表示更多已可用的事件。
title: 從可用字幕資訊中選擇當前字幕資訊
exl-id: d604dedc-f3c3-4c97-9b0f-84da326c0678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 從可用字幕資訊中選擇當前字幕資訊 {#select-a-current-caption-track-from-among-available-tracks}

您可以從當前可用的隱藏字幕字幕字幕字幕資訊清單中選擇一個字幕資訊。 這將成為當前軌道，當可見性開啟時顯示。 某些軌道最初可能不可用，因此請偵聽表示更多已可用的事件。

1. 等待媒體播放器至少位於 `PREPARED` 狀態。
1. 聽聽這些事件：

   * `MediaPlayerEvent.STATUS_CHANGED` 狀態 `MediaPlayerStatus.INITIALIZED`:隱藏字幕軌道的初始清單可用。

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
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. 為指示有更多磁軌可用的事件實現偵聽器。 當TVSDK派單事件時，檢索當前可用軌道清單。

   每次事件發生時檢索清單，以確保始終擁有最新的清單。
