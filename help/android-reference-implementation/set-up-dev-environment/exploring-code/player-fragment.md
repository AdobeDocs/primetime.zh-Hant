---
description: 您可在PlayerFragment類別中編輯程式碼，以建立全功能管理員。
seo-description: 您可在PlayerFragment類別中編輯程式碼，以建立全功能管理員。
seo-title: 播放器片段
title: 播放器片段
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 播放器片段 {#playerfragment}

您可在PlayerFragment類別中編輯程式碼，以建立全功能管理員。

類 `PlayerFragment` 別包含所有UI元件，如 `playerFrame`、 `ControlBar`、 `playerClickableAdFragment`和 `adOverlay`。

它可處理所有這些元件的初始化，以及建立播放器、設定檢視、建立媒體播放器的功能管理員、處理媒體事件（例如繼續、播放和暫停），以及處理 `QoSManager`、 `DRMManager`、 `CCManager`、 `AAManager`、 `AdsManager`、 `PlaybackManager``EntitlementManager`和事件接聽器

包含的配置參數的XML檔案 `PlayerFragment` 為 `res/layout/fragment_player.xml`。

在建立功能管理員之前，您必須先確定檔案中包含下列程式碼，以建立媒體播 `PlayerFragment.java` 放器：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
