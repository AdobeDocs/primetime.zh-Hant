---
description: 可以使用TVSDK檢索可在查找欄上顯示的媒體資訊。
title: 顯示視頻的持續時間、當前時間和剩餘時間
exl-id: 58288501-7d61-4cf3-ae62-d92b83c73a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 顯示視頻的持續時間、當前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

可以使用TVSDK檢索可在查找欄上顯示的媒體資訊。

1. 等待玩家處於「已準備」狀態。
1. 使用 `MediaPlayer.getCurrentTime` 的雙曲餘切值。

   這將返回虛擬時間線上當前播放頭位置（毫秒）。 該時間是相對於可能包含多個替代內容實例的解析流計算的，例如，將多個廣告或廣告片段拼接到主流中。 對於即時/線性流，返回的時間始終在回放窗口範圍內。

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. 檢索流的播放範圍並確定持續時間。
   1. 使用 `mediaPlayer.getPlaybackRange` 方法獲取虛擬時間軸時間範圍。

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. 使用 `mediacore.utils.TimeRange`。
   1. 要確定持續時間，請從範圍結束減去開始。

      這包括插入流（廣告）的附加內容的持續時間。

      對於VOD，範圍始終以零開始，結束值等於主內容持續時間和插入流（廣告）中的附加內容的持續時間之和。

      對於線性/即時資產，該範圍表示回放窗口範圍，且此範圍在回放期間會發生更改。

      TVSDK呼叫 `onUpdated` 回調以指示媒體項已刷新，且其屬性（包括播放範圍）已更新。

1. 使用 `MediaPlayer` 和 `SeekBar` 可在Android SDK中公開提供的類，以設定seek-bar參數。

   例如，此處可能包含 `SeekBar` 2 `TextView` 元素。

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

1. 使用計時器定期檢索當前時間並更新SeekBar。

   以下示例使用 `Clock.java` helper類作為計時器，該計時器在參考播放器MighineReference中可用。 此類設定事件偵聽器並觸發 `onTick` 事件，或您可以指定的另一個超時值。

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   在每個時鐘週期上，此示例檢索媒體播放器的當前位置並更新SeekBar。 它使用兩個TextView元素將當前時間和回放範圍結束位置標籤為數值。

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```
