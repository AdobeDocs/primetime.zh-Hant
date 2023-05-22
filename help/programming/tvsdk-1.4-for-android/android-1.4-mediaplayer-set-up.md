---
description: Android的MediaPlayer介面封裝了媒體播放器的功能和行為。
title: 設定MediaPlayer
exl-id: 2698fe8d-0b73-4aad-9fee-55d034d8ca64
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 設定MediaPlayer {#set-up-the-mediaplayer}

Android的MediaPlayer介面封裝了媒體播放器的功能和行為。

TVSDK提供了 `MediaPlayer` 介面， `DefaultMediaPlayer` 類。 當需要視頻播放功能時，實例化 `DefaultMediaPlayer`。

>[!TIP]
>
>與 `DefaultMediaPlayer` 僅使用由 `MediaPlayer` 。

1. 使用公用實例化MediaPlayer `DefaultMediaPlayer.create` 工廠方法，傳遞Java Android應用程式上下文對象。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 呼叫 `MediaPlayer.getView` 以獲取對 `MediaPlayerView` 實例。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 放置 `MediaPlayerView` 實例 `FrameLayout` 實例，將視頻放在設備的螢幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

的 `MediaPlayer` 實例現在可用，並且已正確配置為在設備螢幕上顯示視頻內容。
