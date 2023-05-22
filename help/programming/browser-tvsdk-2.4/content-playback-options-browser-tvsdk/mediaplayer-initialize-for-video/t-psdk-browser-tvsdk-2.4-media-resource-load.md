---
description: 通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。
title: 在MediaPlayer中載入媒體資源
exl-id: b775c33e-399c-4a03-a132-407944f07706
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 在MediaPlayer中載入媒體資源 {#load-a-media-resource-in-the-mediaplayer}

通過直接實例化MediaResource並載入要播放的視頻內容來載入資源。

1. 設定 `MediaPlayer` 對象的可播放項，以及要播放的新資源。

   替換現有 `MediaPlayer` 通過調用對象的當前可播放項 `replaceCurrentResource` 通過現有 `MediaResource` 實例。

1. 等待瀏覽器TVSDK派單 `AdobePSDK.MediaPlayerStatusChangeEvent` 與 `event.status` 等於以下任何項：

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      通過這些事件，MediaPlayer對象將通知您的應用程式媒體資源是否已成功載入。

1. 當媒體播放器的狀態更改為 `MediaPlayerStatus.INITIALIZED`您可以 `MediaPlayer.prepareToPlay`。

   INITIALIZED狀態表示媒體已成功載入。 呼叫 `prepareToPlay` 啟動廣告解決和投放過程（如果有）。
1. 當瀏覽器TVSDK派單時 `MediaPlayerStatus.PREPARED` 已成功載入媒體流（建立MediaPlayerItem）並準備播放。

如果出現故障， `MediaPlayer` 切換到 `MediaPlayerStatus.ERROR`。

它還通過調度 `MediaPlayerStatus.ERROR` 的子菜單。

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

以下簡化示例代碼說明了載入媒體資源的過程：

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
