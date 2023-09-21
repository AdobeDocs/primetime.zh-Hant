---
description: 將MediaPlayer具現化，並將它的一個檢視置入框架版面中。
title: 設定MediaPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 設定MediaPlay {#set-up-the-mediaplayer}

TVSDK提供的工具可讓您建立進階視訊播放器應用程式（您的Primetime播放器），以便與其他Primetime元件整合。 此外，還提供許多專為最佳化視訊播放品質而設計的功能。

將MediaPlayer具現化，並將它的一個檢視置入框架版面中。

1. 具現化 `MediaPlayer`，傳遞 `android.content.Context` 物件至建構函式：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架配置( `android.widget.FrameLayout`)以保留 `ViewGroup` 之 `mediaPlayer`：

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   以下是要建立的程式碼片段 `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 放置檢視 `mediaPlayer` 框架版面配置內：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>此 `MediaPlayer` 例項( `mediaPlayer`)現已可用，並已正確設定為在裝置熒幕上顯示視訊內容。
