---
description: 您可以使用TVSDK來擷取可顯示在搜尋列上之媒體的相關資訊。
seo-description: 您可以使用TVSDK來擷取可顯示在搜尋列上之媒體的相關資訊。
seo-title: 顯示視訊的持續時間、目前時間和剩餘時間
title: 顯示視訊的持續時間、目前時間和剩餘時間
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 顯示視訊的持續時間、目前時間和剩餘時間{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取可顯示在搜尋列上之媒體的相關資訊。

1. 等待您的播放器處於「已準備」狀態。
1. 使用方法擷取目前的播放頭 `MediaPlayer.getCurrentTime` 時間。

   如此可傳回虛擬時間軸上目前播放磁頭的位置（以毫秒為單位）。 時間會相對於可能包含多個替代內容例項的已解析串流來計算，例如，多個廣告或廣告片段會拼接到主串流中。 對於即時／線性串流，傳回的時間一律在播放視窗範圍內。

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. 擷取串流的播放範圍並決定持續時間。
   1. 使用方 `mediaPlayer.getPlaybackRange` 法來取得虛擬時間軸時間範圍。

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. 使用解析時間範圍 `mediacore.utils.TimeRange`。
   1. 要確定持續時間，請從範圍結束處減去開始。

      這包括插入至串流（廣告）的其他內容的持續時間。

      對於VOD，範圍一律以零開始，而結束值等於主要內容持續時間與插入串流（廣告）中之其他內容的持續時間之和。

      對於線性／即時資產，範圍代表播放視窗範圍，而此範圍在播放期間會變更。

      TVSDK會呼叫 `onUpdated` 您的回呼，指出媒體項目已重新整理，且其屬性（包括播放範圍）已更新。

1. 使用Android SDK中 `MediaPlayer` 公開 `SeekBar` 提供的和類別上可用的方法來設定搜尋列參數。

   例如，以下是可能的版面配置，其中包含 `SeekBar` 和兩個 `TextView` 元素。

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

   下面的示例使用幫 `Clock.java` 助程式類作為計時器，該計時器在參考播放器PrimetimeReference中可用。 此類設定事件偵聽器，並每秒觸發一 `onTick` 個事件，或觸發另一個您可以指定的超時值。

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

   在每個時鐘點上，此範例會擷取媒體播放器的目前位置並更新SeekBar。 它使用兩個TextView元素將當前時間和播放範圍結束位置標籤為數值。

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

