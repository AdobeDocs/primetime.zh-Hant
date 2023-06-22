---
description: 即時開啟一詞是指預先載入一或多個頻道，讓使用者選取頻道或切換頻道時，看到內容立即播放。 在使用者開始觀看時，緩衝已經完成。
title: 立即開啟
exl-id: f640f208-d1b3-467a-be97-38690e10b7ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 立即開啟 {#instant-on}

即時開啟一詞是指預先載入一或多個頻道，讓使用者選取頻道或切換頻道時，看到內容立即播放。 在使用者開始觀看時，緩衝已經完成。

若沒有立即開啟，TVSDK會初始化要播放的媒體，但在應用程式呼叫前不會開始緩衝串流 `play`. 在緩衝完成之前，使用者看不到任何內容。 立即開啟後，您可以啟動多個媒體播放器（或媒體播放器專案載入器）例項，TVSDK就會立即開始緩衝串流。

當使用者變更頻道且資料流已正確緩衝時，呼叫 `play` 會在新頻道上立即開始播放。

雖然數量沒有限制 `MediaPlayer` TVSDK可以執行的例項，執行更多例項會消耗更多資源。 執行中的執行個體數目會影響應用程式效能。 如需這些例項的詳細資訊，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## 設定立即播放的緩衝 {#configure-buffering-for-instant-on-playback}

透過立即開啟，使用者可以切換頻道，並且立即開始播放而無需等候時間。 當您啟用立即開啟時，TVSDK會在開始播放之前緩衝一或多個通道。

1. 透過驗證狀態是否為PREPARED，確認資源已載入並準備好播放。
1. 通話前 `play`，呼叫 `prepareBuffer` 針對每個 `MediaPlayer` 執行個體。

   這樣會啟用立即開啟，這表示TVSDK會開始緩衝，而不會實際播放媒體資源。 TVSDK會傳送 `BUFFERING_COMPLETED` 緩衝區已滿時的事件。

   >[!NOTE]
   >
   >依預設， `prepareBuffer` 和 `prepareToPlay` 設定媒體串流，以從頭開始播放。 若要從另一個位置開始，請將該位置（以毫秒為單位）傳遞至 `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. 當您收到 `BUFFERING_COMPLETE` 事件，開始播放專案或顯示視覺回饋，指出內容已完全緩衝。

   如果您呼叫 `play`，應立即開始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
