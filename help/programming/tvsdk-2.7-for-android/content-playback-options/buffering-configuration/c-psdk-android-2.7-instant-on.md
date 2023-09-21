---
description: 啟用立即開啟表示已預先載入一或多個通道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 在使用者開始觀看時，緩衝已完成。
title: 立即開啟
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 立即開啟 {#instant-on}

啟用立即開啟表示已預先載入一或多個通道。 當使用者選擇頻道或切換頻道時，內容會立即播放。 在使用者開始觀看時，緩衝已完成。

如果沒有立即開啟，TVSDK會初始化要播放的媒體，但在應用程式呼叫之前不會開始緩衝串流 `play`. 在緩衝完成之前，使用者看不到任何內容。 透過「立即開啟」，您可以啟動多個媒體播放器（或媒體播放器專案載入器）例項，而TVSDK會立即開始緩衝串流。 當使用者變更頻道且資料流已正確緩衝時，呼叫 `play` 會在新頻道上立即開始播放。

雖然數量沒有限制 `MediaPlayer` 和 `MediaPlayerItemLoader` TVSDK可以執行的例項，執行更多例項會佔用更多資源。 執行中的執行個體數目可能會影響應用程式效能。 有關詳細資訊 `MediaPlayerItemLoader`，請參閱 [在媒體播放器中載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK不支援單一 `QoSProvider` 以使用兩者 `itemLoader` 和 `MediaPlayer`. 如果客戶使用立即開啟，應用程式需要維護兩個QoS執行個體，並管理兩個執行個體以取得資訊。

有關詳細資訊 `MediaPlayerItemLoader`，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

## 將QoS提供者執行個體新增至mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 建立QoS提供者並附加至 `mediaPlayerItemLoader` 例項

  ```
  // Create an instance of QoSProvider  
  private QOSProvider _qosProvider = new QOSProvider(this._context);  
  
  // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
  // (before calling load API on mediaPlayerItemLoader instance)  
  _qosProvider.attachMediaPlayerItemLoader(this._loader); 
  ```

  播放開始後，請使用 `_qosProvider` 以取得 `timeToLoad` 和 `timeToPrepare` QoSdata。 其餘的QoS量度可透過以下方式擷取： `QoSProvider` 附加至 `mediaPlayer`.

  有關詳細資訊 `MediaPlayerItemLoader`，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## 設定立即開啟的緩衝 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK提供方法和狀態，可讓您搭配媒體資源使用「立即開啟」。

>[!NOTE]
>
>Adobe建議使用 `MediaPlayerItemLoader` 用於InstantOn。 使用 `MediaPlayerItemLoader`，而非 `MediaPlayer`，請參閱media-resource-load-using-mediaplayeritemloader 。

1. 確認資源已載入，且播放器已準備好播放資源。
1. 通話前 `play`，呼叫 `prepareBuffer` 針對每個 `MediaPlayer` 執行個體。

   >[!NOTE]
   >
   >`prepareBuffer` 啟用「立即開啟」，TVSDK就會立即開始緩衝，並分配 `BUFFERING_COMPLETED` 緩衝區已滿時的事件。

   >[!TIP]
   >
   >根據預設， `prepareBuffer` 和 `prepareToPlay` 設定媒體串流，以從頭開始播放。 若要從另一個位置開始，請將該位置（以毫秒為單位）傳遞至 `prepareToPlay`.

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

1. 當您收到 `BUFFERING_COMPLETE` 事件，開始播放專案或顯示視覺化回饋，指出內容已完全緩衝。

   >[!NOTE]
   >
   >如果您呼叫 `play`，應立即開始播放。
