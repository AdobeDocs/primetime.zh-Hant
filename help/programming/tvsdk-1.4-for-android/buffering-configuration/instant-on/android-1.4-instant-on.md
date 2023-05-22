---
description: 即時載入指預載一個或多個頻道，以便用戶選擇頻道或切換頻道可以立即看到內容播放。 在用戶開始監視時，緩衝已完成。
title: 即開
exl-id: f640f208-d1b3-467a-be97-38690e10b7ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 即開 {#instant-on}

即時載入指預載一個或多個頻道，以便用戶選擇頻道或切換頻道可以立即看到內容播放。 在用戶開始監視時，緩衝已完成。

如果沒有即時開啟，TVSDK將初始化要播放的媒體，但在應用程式調用之前不會開始緩衝流 `play`。 在緩衝完成之前，用戶看不到任何內容。 在即時開啟時，您可以啟動多個媒體播放器（或媒體播放器項載入器）實例，TVSDK會立即開始緩衝流。

當用戶更改頻道且流已正確緩衝時，調用 `play` 在新頻道上立即開始播放。

儘管對於 `MediaPlayer` TVSDK可以運行的實例，運行更多實例會消耗更多資源。 應用程式效能可能受運行實例數的影響。 有關這些實例的詳細資訊，請參見 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)。

## 為即時播放配置緩衝 {#configure-buffering-for-instant-on-playback}

在即時開啟時，用戶可以切換頻道，播放立即開始，而無需等待時間。 啟用即時時，TVSDK會在播放開始之前緩衝一個或多個頻道。

1. 通過驗證狀態是否為PREPARED，確認資源已載入並已準備好播放。
1. 呼叫前 `play`調用 `prepareBuffer` 每 `MediaPlayer` 實例。

   這將啟用即時，這意味著TVSDK開始緩衝，而不實際播放媒體資源。 TVSDK派單 `BUFFERING_COMPLETED` 緩衝區已滿時的事件。

   >[!NOTE]
   >
   >預設情況下， `prepareBuffer` 和 `prepareToPlay` 設定媒體流以從頭開始播放。 要從另一個位置開始，請將該位置（以毫秒為單位）傳遞到 `prepareToPlay`。

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

1. 當您收到 `BUFFERING_COMPLETE` 事件，開始播放項目或顯示可視反饋以指示內容已完全緩衝。

   如果你打電話 `play`，應立即開始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
