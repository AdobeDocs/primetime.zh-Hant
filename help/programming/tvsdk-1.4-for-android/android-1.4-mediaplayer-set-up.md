---
description: Android適用的MediaPlayer介面會封裝媒體播放器的功能和行為。
title: 設定MediaPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 設定MediaPlay {#set-up-the-mediaplayer}

Android適用的MediaPlayer介面會封裝媒體播放器的功能和行為。

TVSDK提供以下實作之一 `MediaPlayer` 介面， `DefaultMediaPlayer` 類別。 當您需要視訊播放功能時，請例項化 `DefaultMediaPlayer`.

>[!TIP]
>
>與 `DefaultMediaPlayer` 僅使用下列方式公開的方法執行個體： `MediaPlayer` 介面。

1. 使用公用程式例項化MediaPlayer `DefaultMediaPlayer.create` Factory方法，傳遞Java Android應用程式內容物件。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 呼叫 `MediaPlayer.getView` 以取得 `MediaPlayerView` 執行個體。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 放置 `MediaPlayerView` 中的執行個體 `FrameLayout` 例項，將視訊放置在裝置的熒幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

此 `MediaPlayer` 執行個體現在可供使用，並已正確設定為在裝置熒幕上顯示視訊內容。
