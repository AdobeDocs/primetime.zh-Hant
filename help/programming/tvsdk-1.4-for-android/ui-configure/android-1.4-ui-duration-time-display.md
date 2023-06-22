---
description: 您可以使用TVSDK來擷取可以顯示在搜尋列上的媒體資訊。
title: 顯示視訊的持續時間、目前時間和剩餘時間
exl-id: 58288501-7d61-4cf3-ae62-d92b83c73a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 顯示視訊的持續時間、目前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取可以顯示在搜尋列上的媒體資訊。

1. 等候您的播放器處於準備狀態。
1. 使用擷取目前的播放點時間 `MediaPlayer.getCurrentTime` 方法。

   這會傳回虛擬時間軸上目前的播放點位置（以毫秒為單位）。 此時間是相對於已解析資料流來計算的，該資料流可能包含替代內容的多個例項，例如拼接至主資料流的多個廣告或廣告插播。 對於即時/線性串流，傳回的時間一律在播放視窗範圍內。

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. 擷取資料流的播放範圍並決定持續時間。
   1. 使用 `mediaPlayer.getPlaybackRange` 取得虛擬時間軸時間範圍的方法。

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. 剖析時間範圍，使用 `mediacore.utils.TimeRange`.
   1. 若要判斷持續時間，請從範圍的結尾減去開始時間。

      這包括插入資料流（廣告）中之其他內容的持續時間。

      對於VOD，範圍一律從零開始，而結束值等於主要內容持續時間與插入串流（廣告）中之其他內容持續時間的總和。

      對於線性/即時資產，範圍表示播放視窗範圍，此範圍在播放期間會變更。

      TVSDK會呼叫您的 `onUpdated` 回撥表示媒體專案已重新整理，而且其屬性（包括播放範圍）已更新。

1. 使用上的可用方法 `MediaPlayer` 和 `SeekBar` 在Android SDK中公開可用以設定搜尋列引數的類別。

   例如，以下是包含下列內容的可能版面： `SeekBar` 和兩個 `TextView` 元素。

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

1. 使用計時器定期擷取目前時間並更新SeekBar。

   以下範例使用 `Clock.java` helper類別做為計時器，可在參考播放器PrimetimeReference中使用。 此類別會設定事件接聽程式，並觸發 `onTick` 事件每秒，或是您可以指定的另一個逾時值。

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

   在每個時鐘刻度上，此範例會擷取媒體播放器的目前位置，並更新SeekBar。 它使用兩個TextView元素將目前時間和播放範圍結束位置標示為數值。

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
