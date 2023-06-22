---
description: Android的MediaPlayer介面會封裝媒體播放器的功能和行為。
title: 設定MediaPlay
exl-id: 2698fe8d-0b73-4aad-9fee-55d034d8ca64
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 設定MediaPlay {#set-up-the-mediaplayer}

Android的MediaPlayer介面會封裝媒體播放器的功能和行為。

TVSDK提供 `MediaPlayer` 介面， `DefaultMediaPlayer` 類別。 當您需要視訊播放功能時，請具現化 `DefaultMediaPlayer`.

>[!TIP]
>
>與 `DefaultMediaPlayer` 執行個體只能使用下列專案公開的方法： `MediaPlayer` 介面。

1. 使用公用程式例項化MediaPlayer `DefaultMediaPlayer.create` factory方法，傳遞Java Android應用程式內容物件。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 呼叫 `MediaPlayer.getView` 以取得 `MediaPlayerView` 執行個體。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 放置 `MediaPlayerView` 中的執行個體 `FrameLayout` 例項，將視訊放在裝置的熒幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

此 `MediaPlayer` 執行個體現在可供使用，並已正確設定為在裝置畫面上顯示視訊內容。
