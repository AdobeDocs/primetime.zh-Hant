---
description: 您可以使用TVSDK來擷取播放器在媒體中的位置資訊，並在搜尋列上顯示。
title: 顯示視訊的持續時間、目前時間和剩餘時間
exl-id: d9832f19-c2d1-413a-b094-091052912c96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 顯示視訊的持續時間、目前時間和剩餘時間 {#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK來擷取播放器在媒體中的位置資訊，並在搜尋列上顯示。

1. 等待播放器至少處於「已準備」狀態。
1. 使用 `MediaPlayer.getCurrentTime` 方法。

   這會傳回虛擬時間軸上目前的播放點位置（以毫秒為單位）。 時間會相對於解析的資料流計算，該資料流可能包含多個替代內容的例項，例如拼接至主資料流的多個廣告或廣告插播。 對於即時/線性資料流，傳回的時間一律在播放視窗範圍內。

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 擷取資料流的播放範圍並決定持續時間。
   1. 使用 `MediaPlayer.getPlaybackRange` 獲取虛擬時間軸時間範圍的方法。

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 使用 `MediaPlayer.getPlaybackRange` 獲取虛擬時間軸時間範圍的方法。

      * 對於VOD，範圍一律以零開始，而結束值等於主要內容持續時間與資料流（廣告）中其他內容持續時間的總和。
      * 對於線性/即時資產，範圍代表播放視窗範圍。 播放期間此範圍會變更。

         TVSDK呼叫 `ITEM_Updated` 回撥，指出媒體項目已重新整理，其屬性（包括播放範圍）已更新。

1. 使用上可用的方法 `MediaPlayer` 和 `SeekBar` 類別，以設定搜尋列參數。

   例如，以下是可能的版面，其中包含搜尋列和兩個 `TextView` 元素。

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

1. 使用計時器定期擷取目前時間並更新搜尋列，如圖所示：

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   下列範例使用 `Clock.java` 幫助類，可在 `ReferencePlayer`，作為計時器。 此類設定事件偵聽器並觸發 `onTick` 事件，或您可指定的其他逾時值。

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

   此範例會在每個時鐘勾號上擷取媒體播放器的目前位置，並更新搜尋列。 它使用兩個 `TextView` 將目前時間和播放範圍結束位置標示為數值的元素。

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
