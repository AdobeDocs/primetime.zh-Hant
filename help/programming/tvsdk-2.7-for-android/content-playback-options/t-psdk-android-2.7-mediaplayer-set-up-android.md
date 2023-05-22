---
description: 實例化MediaPlayer並將其視圖放入幀佈局中。
title: 設定MediaPlayer
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 設定MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供用於建立高級視頻播放器應用程式（您的Mighide播放器）的工具，您可以與其他Mighide元件整合。 它還提供了多種功能，旨在最大限度地提高視頻播放的質量。

實例化MediaPlayer並將其視圖放入幀佈局中。

1. 實例化 `MediaPlayer`，通過 `android.content.Context` 對象到建構子：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架佈局( `android.widget.FrameLayout`) `ViewGroup` 共 `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   下面是要建立的代碼段 `_viewGroup`。

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 放置視圖 `mediaPlayer` 框架佈局內：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>的 `MediaPlayer` 實例( `mediaPlayer`)現在可用，並且已正確配置以在設備螢幕上顯示視頻內容。
