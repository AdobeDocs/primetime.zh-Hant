---
description: 您可以使用TVSDK來擷取有關播放器在媒體中位置的資訊，並在搜尋列上顯示。
title: 顯示視訊的持續時間、目前時間和剩餘時間
exl-id: 68501c81-346a-4c3e-aa20-a98b8b1c6b17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 顯示視訊的持續時間、目前時間和剩餘時間 {#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取有關播放器在媒體中位置的資訊，並在搜尋列上顯示。

1. 等候播放器至少處於PREPARED狀態。
1. 使用擷取目前的播放點時間 `MediaPlayer.getCurrentTime` 方法。

   這會傳回虛擬時間軸上目前的播放點位置（以毫秒為單位）。 此時間是相對於已解析資料流來計算的，該資料流可能包含替代內容的多個例項，例如拼接至主資料流的多個廣告或廣告插播。 對於即時/線性串流，傳回的時間一律在播放視窗範圍內。

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
      * 對於線性/即時資產，範圍表示播放視窗範圍。 此範圍會在播放期間變更。

         TVSDK呼叫 `ITEM_Updated` 回撥表示媒體專案已重新整理，而且其屬性（包括播放範圍）已更新。

1. 使用上的可用方法 `MediaPlayer` 並在 `SeekBar` 類別來設定搜尋列引數。

   例如，以下是可能的配置，其中包含搜尋列和兩個 `TextView` 元素。

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

   以下範例使用 `Clock.java` helper類別，可在 `ReferencePlayer`，做為計時器。 此類別會設定事件接聽程式，並觸發 `onTick` 事件每秒，或是您可以指定的另一個逾時值。

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

   在每個時鐘滴答中，此範例會擷取媒體播放器目前的位置，並更新搜尋列。 它會使用兩個 `TextView` 元素來將目前時間和播放範圍結束位置標示為數值。

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
