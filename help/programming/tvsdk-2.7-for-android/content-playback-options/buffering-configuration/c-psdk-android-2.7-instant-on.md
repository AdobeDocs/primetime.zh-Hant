---
description: 立即啟用表示已預先載入一或多個頻道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 緩衝在用戶開始監視時完成。
seo-description: 立即啟用表示已預先載入一或多個頻道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 緩衝在用戶開始監視時完成。
seo-title: 立即啟動
title: 立即啟動
uuid: 7e14b779-2a36-4ff4-a365-9ac49a836ff3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# 立即啟動{#instant-on}

立即啟用表示已預先載入一或多個頻道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 緩衝在用戶開始監視時完成。

若沒有立即啟動，TVSDK會初始化要播放的媒體，但直到應用程式呼叫`play`時，才會開始緩衝串流。 在緩衝完成之前，使用者不會看到任何內容。 有了Instant On，您可以啟動多個媒體播放器（或媒體播放器項目載入器）例項，而TVSDK會立即開始緩衝串流。 當使用者變更頻道且串流已正確緩衝時，在新頻道上呼叫`play`會立即開始播放。

雖然TVSDK可執行的`MediaPlayer`和`MediaPlayerItemLoader`例項數目沒有限制，但執行更多例項會耗用更多資源。 應用程式效能可能會受執行中的例項數所影響。 如需`MediaPlayerItemLoader`的詳細資訊，請參閱[在媒體播放器中載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)。

>[!IMPORTANT]
>
>TVSDK不支援單一`QoSProvider`搭配`itemLoader`和`MediaPlayer`使用。 如果客戶使用Instant On，應用程式需要維護兩個QoS實例並管理這兩個實例以獲取資訊。

如需`MediaPlayerItemLoader`的詳細資訊，請參閱[使用MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)載入媒體資源。

## 新增QoS提供者例項至mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 建立QoS提供器並將其附加到`mediaPlayerItemLoader`實例

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   播放開始後，使用`_qosProvider`獲取`timeToLoad`和`timeToPrepare` QoSdata。 剩餘的QoS度量可以使用附加到`mediaPlayer`的`QoSProvider`來檢索。

   如需`MediaPlayerItemLoader`的詳細資訊，請參閱[使用MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader)載入媒體資源。

## 為Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}配置緩衝

TVSDK提供方法和狀態，允許您將「立即啟動」與媒體資源搭配使用。

>[!NOTE]
>
>Adobe建議使用`MediaPlayerItemLoader`作為InstantOn。 若要使用`MediaPlayerItemLoader`而非`MediaPlayer`，請參閱media-resource-load-using-mediaplayeritemloader。

1. 確認已載入資源，且播放器已準備播放資源。
1. 在呼叫`play`之前，請呼叫每個`MediaPlayer`實例的`prepareBuffer`。

   >[!NOTE]
   >
   >`prepareBuffer` 啟用Instant On，而TVSDK會立即開始緩衝，並在緩衝 `BUFFERING_COMPLETED` 區已滿時分派事件。

   >[!TIP]
   >
   >依預設，`prepareBuffer`和`prepareToPlay`會設定媒體串流，從頭開始播放。 若要從另一個位置開始，請將位置（以毫秒為單位）傳遞至`prepareToPlay`。

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

1. 當您收到`BUFFERING_COMPLETE`事件時，請開始播放項目或顯示視覺化回應，以指出內容已完全緩衝。

   >[!NOTE]
   >
   >如果您呼叫`play`，應立即開始播放。

