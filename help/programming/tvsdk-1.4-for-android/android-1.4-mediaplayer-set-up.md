---
description: Android專用的MediaPlayer介面可封裝媒體播放器的功能與行為。
seo-description: Android專用的MediaPlayer介面可封裝媒體播放器的功能與行為。
seo-title: 設定MediaPlayer
title: 設定MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 設定MediaPlayer {#set-up-the-mediaplayer}

Android專用的MediaPlayer介面可封裝媒體播放器的功能與行為。

TVSDK提供介面的一 `MediaPlayer` 種實作， `DefaultMediaPlayer` 類別。 當您需要視訊播放功能時，請執行個體化 `DefaultMediaPlayer`。

>[!TIP]
>
>僅與介 `DefaultMediaPlayer` 面公開的方法互動實 `MediaPlayer` 例。

1. 使用公用工廠方法執行個 `DefaultMediaPlayer.create` 體化MediaPlayer，並傳遞Java Android應用程式內容物件。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 呼叫 `MediaPlayer.getView` 以取得例項的參 `MediaPlayerView` 考。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 將執 `MediaPlayerView` 行個體放 `FrameLayout` 入執行個體，將視訊置於裝置的螢幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

現在 `MediaPlayer` 可使用此例項，並正確設定以在裝置螢幕上顯示視訊內容。
