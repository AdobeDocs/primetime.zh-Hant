---
description: 您可在PlayerFragment類別中編輯程式碼，以建立全功能管理員。
title: 播放器片段
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

您可在PlayerFragment類別中編輯程式碼，以建立全功能管理員。

`PlayerFragment`類別包含所有UI元件，例如`playerFrame`、`ControlBar`、`playerClickableAdFragment`和`adOverlay`。

它可處理所有這些元件的初始化，以及建立播放器、設定檢視、建立媒體播放器的功能管理程式、處理媒體事件，例如繼續、播放和暫停，並處理`QoSManager`、`DRMManager`、`CCManager`、`AAManager`、`AdsManager`、`PlaybackManager`和`EntitlementManager`的事件監聽程式。

包含`PlayerFragment`配置參數的XML檔案為`res/layout/fragment_player.xml`。

在建立功能管理員之前，您必須先確定`PlayerFragment.java`檔案中包含下列程式碼，以建立媒體播放器：

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
