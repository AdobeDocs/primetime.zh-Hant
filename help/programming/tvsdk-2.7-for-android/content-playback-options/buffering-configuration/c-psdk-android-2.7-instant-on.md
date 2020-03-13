---
description: 立即啟用表示已預先載入一或多個頻道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 緩衝在用戶開始監視時完成。
seo-description: 立即啟用表示已預先載入一或多個頻道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 緩衝在用戶開始監視時完成。
seo-title: 立即啟動
title: 立即啟動
uuid: 7e14b779-2a36-4ff4-a365-9ac49a836ff3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 立即啟動 {#instant-on}

立即啟用表示已預先載入一或多個頻道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 緩衝在用戶開始監視時完成。

若沒有「立即啟動」,TVSDK會初始化要播放的媒體，但在應用程式呼叫前不會開始緩衝串流 `play`。 在緩衝完成之前，使用者不會看到任何內容。 有了Instant On，您可以啟動多個媒體播放器（或媒體播放器項目載入器）例項，而TVSDK會立即開始緩衝串流。 當使用者變更頻道且串流已正確緩衝時，新頻道上的呼 `play` 叫會立即開始播放。

雖然TVSDK可執行的例項和 `MediaPlayer` 例項 `MediaPlayerItemLoader` 數目沒有限制，但執行更多例項會耗用更多資源。 應用程式效能可能會受執行中的例項數所影響。 如需詳細資訊， `MediaPlayerItemLoader`請參 [閱在媒體播放器中載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)。

>[!IMPORTANT]
>
>TVSDK不支援單一軟體 `QoSProvider` 搭配和 `itemLoader` 運作 `MediaPlayer`。 如果客戶使用Instant On，應用程式需要維護兩個QoS實例並管理這兩個實例以獲取資訊。

如需詳細資訊， `MediaPlayerItemLoader`請參 [閱使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)。

## 新增QoS提供者例項至mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 建立QoS提供器並將其附加到實 `mediaPlayerItemLoader` 例

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   播放開始後，請使 `_qosProvider` 用來取得 `timeToLoad` 和 `timeToPrepare` QoSdata。 剩餘的QoS度量可以使用附加 `QoSProvider` 到的來檢索 `mediaPlayer`。

   如需詳細資訊， `MediaPlayerItemLoader`請參 [閱使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader)。

## 配置立即啟動的緩衝 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK提供方法和狀態，允許您將「立即啟動」與媒體資源搭配使用。

>[!NOTE]
>
>Adobe建議使 `MediaPlayerItemLoader` 用InstantOn。 若要使 `MediaPlayerItemLoader`用(而非 `MediaPlayer`使用)media-resource-load-using-mediaplayeritemloader。

1. 確認已載入資源，且播放器已準備播放資源。
1. 在呼叫 `play`前，請呼 `prepareBuffer` 叫每個 `MediaPlayer` 例項。

   >[!NOTE]
   >
   >`prepareBuffer` 啟用Instant On，而TVSDK會立即開始緩衝，並在緩衝 `BUFFERING_COMPLETED` 區已滿時分派事件。

   >[!TIP]
   >
   >依預設， `prepareBuffer` 並 `prepareToPlay` 設定媒體串流，從頭開始播放。 若要從另一個位置開始，請將位置（以毫秒為單位）傳遞至 `prepareToPlay`。

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. 當您收到事 `BUFFERING_COMPLETE` 件時，請開始播放項目或顯示視覺化回應，以指出內容已完全緩衝。

   >[!NOTE]
   >
   >如果您呼叫 `play`，應立即開始播放。

