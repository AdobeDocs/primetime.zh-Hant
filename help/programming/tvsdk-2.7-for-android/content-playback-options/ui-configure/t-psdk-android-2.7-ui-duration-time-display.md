---
description: 您可以使用TVSDK來擷取播放器在媒體中位置的資訊，並在搜尋列上顯示。
seo-description: 您可以使用TVSDK來擷取播放器在媒體中位置的資訊，並在搜尋列上顯示。
seo-title: 顯示視訊的持續時間、目前時間和剩餘時間
title: 顯示視訊的持續時間、目前時間和剩餘時間
uuid: 13627fa2-8cd8-4336-bc4b-7e3226330389
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 顯示視訊的持續時間、目前時間和剩餘時間 {#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取播放器在媒體中位置的資訊，並在搜尋列上顯示。

1. 等待玩家至少處於「已準備」狀態。
1. 使用方法擷取目前的播放頭 `MediaPlayer.getCurrentTime` 時間。

   如此可傳回虛擬時間軸上目前播放磁頭的位置（以毫秒為單位）。 時間會相對於可能包含多個替代內容例項的已解析串流來計算，例如，多個廣告或廣告片段會拼接到主串流中。 對於即時／線性串流，傳回的時間一律在播放視窗範圍內。

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 擷取串流的播放範圍並決定持續時間。
   1. 使用方 `MediaPlayer.getPlaybackRange` 法來取得虛擬時間軸時間範圍。

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 使用方 `MediaPlayer.getPlaybackRange` 法來取得虛擬時間軸時間範圍。

      * 對於VOD，範圍一律以零開始，而結束值等於主要內容持續時間與串流（廣告）中其他內容的持續時間之和。
      * 對於線性／即時資產，範圍代表播放視窗範圍。 播放時，此範圍會變更。

         TVSDK呼叫回 `ITEM_Updated` 呼以指出媒體項目已重新整理，且其屬性（包括播放範圍）已更新。

1. 使用Android SDK中類別 `MediaPlayer` 上和類 `SeekBar` 別上可用的方法來設定搜尋列參數。

   例如，以下是可能的版面配置，其中包含搜尋列和兩個 `TextView` 元素。

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

1. 使用計時器定期檢索當前時間並更新搜索欄，如圖所示：

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width=&quot;477.000pt&quot;}

   以下示例使用 `Clock.java` Helper類(在中可 `ReferencePlayer`用)作為計時器。 此類設定事件偵聽器，並每秒觸發一 `onTick` 個事件，或觸發另一個您可以指定的超時值。

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

   在每個時鐘點上，此範例會擷取媒體播放器的目前位置並更新搜尋列。 它使用兩個 `TextView` 元素將目前時間和播放範圍結束位置標示為數值。

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

