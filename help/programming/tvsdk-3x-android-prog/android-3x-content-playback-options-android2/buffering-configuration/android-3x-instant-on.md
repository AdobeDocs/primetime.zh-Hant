---
description: 啟用即時開啟意味著預載入一個或多個通道。 當用戶選擇頻道或切換頻道時，內容會立即播放。 在用戶開始監視時，緩衝已完成。
title: 即時開啟
exl-id: 59293e07-160a-41a2-8ffe-7ca9323048f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 即時開啟 {#instant-on}

啟用即時開啟意味著預載入一個或多個通道。 當用戶選擇頻道或切換頻道時，內容會立即播放。 在用戶開始監視時，緩衝已完成。

如果沒有「即時開啟」，TVSDK將初始化要播放的媒體，但在應用程式調用之前不會開始緩衝流 `play`。 在緩衝完成之前，用戶看不到任何內容。 使用「即時開啟」，可以啟動多個媒體播放器（或媒體播放器項載入器）實例，TVSDK將立即開始緩衝流。 當用戶更改頻道且流已正確緩衝時，調用 `play` 在新頻道上立即開始播放。

儘管對於 `MediaPlayer` 和 `MediaPlayerItemLoader` TVSDK可以運行的實例，運行更多實例會消耗更多資源。 應用程式效能可能受正在運行的實例數的影響。 有關 `MediaPlayerItemLoader`，請參閱 [在媒體播放器中載入媒體資源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)。

>[!IMPORTANT]
>
>TVSDK不支援單個 `QoSProvider` 與兩者合作 `itemLoader` 和 `MediaPlayer`。 如果客戶使用「即時開機」，則應用程式需要維護兩個QoS實例並管理兩個實例以獲取資訊。

有關 `MediaPlayerItemLoader`，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md)。

## 將QoS提供程式實例添加到mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 建立QoS提供程式並將其連接到 `mediaPlayerItemLoader` 實例

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   播放開始後，使用 `_qosProvider` 要 `timeToLoad` 和 `timeToPrepare` QoS資料。 剩餘的QoS度量可通過使用 `QoSProvider` 與 `mediaPlayer`。

   有關 `MediaPlayerItemLoader`，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md)。

## 為「即時開啟」配置緩衝 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK提供了允許您將「即時開啟」與媒體資源一起使用的方法和狀態。

>[!NOTE]
>
>Adobe建議使用 `MediaPlayerItemLoader` 即時開啟。 要使用 `MediaPlayerItemLoader`，而不是 `MediaPlayer`，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md)。

1. 確認已載入資源，並且播放器準備播放該資源。
1. 呼叫前 `play`調用 `prepareBuffer` 每 `MediaPlayer` 實例。

   `prepareBuffer` 啟用即時開啟，TVSDK立即開始緩衝並調度 `BUFFERING_COMPLETED` 緩衝區已滿時的事件。

   >[!TIP]
   >
   >預設情況下， `prepareBuffer` 和 `prepareToPlay` 設定媒體流以從頭開始播放。 要從另一個位置開始，請將該位置（以毫秒為單位）傳遞給 `prepareToPlay`。

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

1. 當您收到 `BUFFERING_COMPLETE` 事件，開始播放項目或顯示可視反饋以指示內容已完全緩衝。

   >[!NOTE]
   >
   >如果你打電話 `play`，應立即開始播放。
