---
description: 您可以使用TVSDK來擷取有關播放器在媒體中位置的資訊，並將其顯示在搜尋列上。
title: 顯示視訊的持續時間、目前時間和剩餘時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 顯示視訊的持續時間、目前時間和剩餘時間 {#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取有關播放器在媒體中位置的資訊，並將其顯示在搜尋列上。

1. 等候播放器至少處於「已準備」狀態。
1. 使用擷取目前的播放點時間 `MediaPlayer.getCurrentTime` 方法。

   這會傳回虛擬時間軸上目前的播放點位置（以毫秒為單位）。 此時間是相對於已解析資料流而計算的，該資料流可能包含多個替代內容的例項，例如多個廣告或拼接到主資料流中的廣告插播。 對於即時/線性串流，傳回的時間一律在播放視窗範圍內。

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 擷取資料流的播放範圍並決定持續時間。
   1. 使用 `MediaPlayer.getPlaybackRange` 取得虛擬時間軸時間範圍的方法。

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 使用 `MediaPlayer.getPlaybackRange` 取得虛擬時間軸時間範圍的方法。

      * 對於VOD，範圍一律從零開始，而結束值等於主要內容持續時間與串流（廣告）中其他內容持續時間的和。
      * 對於線性/即時資產，範圍表示播放視窗範圍。 播放期間，此範圍會變更。

        TVSDK呼叫 `ITEM_Updated` 回呼表示媒體專案已重新整理，而且其屬性（包括播放範圍）已更新。

1. 使用上的可用方法 `MediaPlayer` 並在 `SeekBar` 類別來設定搜尋列引數。

   例如，以下是包含搜尋列和兩個的可能版面 `TextView` 元素。

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. 使用計時器定期擷取目前時間並更新搜尋列，如下圖所示：

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   以下範例使用 `Clock.java` helper類別，可在 `ReferencePlayer`，作為計時器。 此類別會設定事件監聽器，並觸發 `onTick` 每秒發生一次事件，或是您可以指定的另一個逾時值。

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   在每個時鐘刻度上，此範例會擷取媒體播放器目前的位置，並更新搜尋列。 它會使用兩個 `TextView` 元素來將目前時間和播放範圍結束位置標示為數值。

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
