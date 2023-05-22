---
description: 可以使用TVSDK檢索有關播放器在媒體中位置的資訊，並在查找欄上顯示。
title: 顯示視頻的持續時間、當前時間和剩餘時間
exl-id: 68501c81-346a-4c3e-aa20-a98b8b1c6b17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 顯示視頻的持續時間、當前時間和剩餘時間 {#display-the-duration-current-time-and-remaining-time-of-the-video}

可以使用TVSDK檢索有關播放器在媒體中位置的資訊，並在查找欄上顯示。

1. 等待玩家至少處於PREPARED狀態。
1. 使用 `MediaPlayer.getCurrentTime` 的雙曲餘切值。

   這將返回虛擬時間線上當前播放頭位置（毫秒）。 該時間是相對於可能包含多個替代內容實例的解析流計算的，例如，將多個廣告或廣告片段拼接到主流中。 對於即時/線性流，返回的時間始終在回放窗口範圍內。

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 檢索流的播放範圍並確定持續時間。
   1. 使用 `MediaPlayer.getPlaybackRange` 方法獲取虛擬時間軸時間範圍。

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 使用 `MediaPlayer.getPlaybackRange` 方法獲取虛擬時間軸時間範圍。

      * 對於VOD，該範圍始終以零開始，並且結束值等於主內容持續時間和流（廣告）中附加內容持續時間之和。
      * 對於線性/即時資產，該範圍表示回放窗口範圍。 在回放期間，此範圍會發生更改。

         TVSDK調用 `ITEM_Updated` 回調，以指示媒體項已刷新，並且其屬性（包括播放範圍）已更新。

1. 使用上可用的方法 `MediaPlayer` 在 `SeekBar` 類在Android SDK中設定查找條參數。

   例如，這裡可能有一個佈局，它包含查找欄和兩個 `TextView` 元素。

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

1. 使用計時器定期檢索當前時間並更新查找欄，如圖所示：

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   以下示例使用 `Clock.java` 幫助程式類，在 `ReferencePlayer`，作為計時器。 此類設定事件偵聽器並觸發 `onTick` 事件，或您可以指定的另一個超時值。

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

   在每個時鐘週期上，此示例檢索媒體播放器的當前位置並更新查找欄。 它使用 `TextView` 將當前時間和回放範圍結束位置標籤為數值的元素。

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
