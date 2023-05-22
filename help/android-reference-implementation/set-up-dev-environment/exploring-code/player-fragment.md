---
description: PlayerFragment類是編輯代碼以建立完全啟用的功能管理器的位置。
title: 播放器片段
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 播放器片段 {#playerfragment}

PlayerFragment類是編輯代碼以建立完全啟用的功能管理器的位置。

的 `PlayerFragment` 類包含所有UI元件，如 `playerFrame`。 `ControlBar`。 `playerClickableAdFragment`, `adOverlay`。

它處理所有這些元件的初始化以及建立播放器、設定視圖、為媒體播放器建立功能管理器、處理媒體事件（如恢復、播放和暫停）和處理事件偵聽器 `QoSManager`。 `DRMManager`。 `CCManager`。 `AAManager`。 `AdsManager`。 `PlaybackManager`, `EntitlementManager`。

包含XML的配置參數的XML檔案 `PlayerFragment` 是 `res/layout/fragment_player.xml`。

在建立功能管理器之前，您需要通過以下代碼位於 `PlayerFragment.java` 檔案：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
