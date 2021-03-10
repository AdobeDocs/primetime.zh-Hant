---
description: 執行個體化MediaPlayer，並將其檢視置入影格版面。
title: 設定MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 設定MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），讓您可與其他Primetime元件整合。 此外，它還提供多種功能，可讓視訊播放品質發揮最大。

執行個體化MediaPlayer，並將其檢視置入影格版面。

1. 實例化`MediaPlayer`，將`android.content.Context`物件傳遞至建構函式：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供影格版面(`android.widget.FrameLayout`)以容納`mediaPlayer`的`ViewGroup`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   以下是建立`_viewGroup`的程式碼片段。

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 將`mediaPlayer`的檢視置於影格版面中：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>`MediaPlayer`例項(`mediaPlayer`)現已可用，並已正確設定以在裝置螢幕上顯示視訊內容。