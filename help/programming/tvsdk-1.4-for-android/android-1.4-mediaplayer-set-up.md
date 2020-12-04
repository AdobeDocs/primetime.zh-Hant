---
description: Android專用的MediaPlayer介面可封裝媒體播放器的功能與行為。
seo-description: Android專用的MediaPlayer介面可封裝媒體播放器的功能與行為。
seo-title: 設定MediaPlayer
title: 設定MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 設定MediaPlayer {#set-up-the-mediaplayer}

Android專用的MediaPlayer介面可封裝媒體播放器的功能與行為。

TVSDK提供`MediaPlayer`介面（`DefaultMediaPlayer`類別）的一個實作。 當您需要視訊播放功能時，請執行個體化`DefaultMediaPlayer`。

>[!TIP]
>
>只與`DefaultMediaPlayer`介面公開的方法交互。`MediaPlayer`

1. 使用公用`DefaultMediaPlayer.create`工廠方法執行個體化MediaPlayer，並傳遞Java Android應用程式內容物件。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 呼叫`MediaPlayer.getView`以取得對`MediaPlayerView`例項的參考。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 將`MediaPlayerView`實例放在`FrameLayout`實例中，該實例將視頻放在設備螢幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

`MediaPlayer`例項現已可用，並已正確設定，可在裝置螢幕上顯示視訊內容。
