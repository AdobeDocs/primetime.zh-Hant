---
description: 「立即開啟」一詞指預先載入一或多個頻道，讓選擇頻道或切換頻道的使用者可立即看到內容播放。 緩衝已在使用者開始觀看時完成。
seo-description: 「立即開啟」一詞指預先載入一或多個頻道，讓選擇頻道或切換頻道的使用者可立即看到內容播放。 緩衝已在使用者開始觀看時完成。
seo-title: 立即啟動
title: 立即啟動
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 即時於{#instant-on}

「立即開啟」一詞指預先載入一或多個頻道，讓選擇頻道或切換頻道的使用者可立即看到內容播放。 緩衝已在使用者開始觀看時完成。

在不立即啟動的情況下，TVSDK會初始化要播放的媒體，但直到應用程式呼叫`play`時，才會開始緩衝串流。 在緩衝完成之前，使用者不會看到任何內容。 立即啟動後，您就可啟動多個媒體播放器（或媒體播放器項目載入器）例項，而TVSDK會立即開始緩衝串流。

當使用者變更頻道且串流已正確緩衝時，在新頻道上呼叫`play`會立即開始播放。

雖然TVSDK可執行的`MediaPlayer`例項數目沒有限制，但執行更多例項會耗用更多資源。 執行中的執行個體數量會影響應用程式效能。 如需這些例項的詳細資訊，請參閱[使用MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)載入媒體資源。

## 配置即時播放{#configure-buffering-for-instant-on-playback}的緩衝

使用者可立即開啟，以切換頻道，而不需等待時間，就可立即開始播放。 當您啟用立即啟動時，TVSDK會在播放開始前緩衝一或多個頻道。

1. 通過驗證狀態為PREPARED，確認資源已載入並已準備好播放。
1. 在呼叫`play`之前，請呼叫每個`MediaPlayer`實例的`prepareBuffer`。

   如此可立即啟動，表示TVSDK會開始緩衝，而不實際播放媒體資源。 當緩衝區已滿時，TVSDK會調度`BUFFERING_COMPLETED`事件。

   >[!NOTE]
   >
   >依預設，`prepareBuffer`和`prepareToPlay`會設定媒體串流，從頭開始播放。 若要從另一個位置開始，請將位置（以毫秒為單位）傳遞至`prepareToPlay`。

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

1. 當您收到`BUFFERING_COMPLETE`事件時，請開始播放項目或顯示視覺化回應，以指出內容已完全緩衝。

   如果您呼叫`play`，應立即開始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
