---
description: 您可以在PlayerFragment類別中編輯程式碼，以建立完全啟用的功能管理員。
title: Playerfragment
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Playerfragment {#playerfragment}

您可以在PlayerFragment類別中編輯程式碼，以建立完全啟用的功能管理員。

此 `PlayerFragment` 類別包含所有UI元件，例如 `playerFrame`， `ControlBar`， `playerClickableAdFragment`、和 `adOverlay`.

它會處理所有這些元件的初始化，以及建立播放器、設定檢視、建立媒體播放器的功能管理員、處理媒體事件（例如繼續、播放和暫停）和處理事件接聽程式 `QoSManager`， `DRMManager`， `CCManager`， `AAManager`， `AdsManager`， `PlaybackManager`、和 `EntitlementManager`.

包含組態引數的XML檔案 `PlayerFragment` 是 `res/layout/fragment_player.xml`.

建立功能管理員之前，您必須先建立媒體播放器，確認下列程式碼位於 `PlayerFragment.java` 檔案：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
