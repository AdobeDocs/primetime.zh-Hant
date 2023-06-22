---
description: 將MediaPlayer例項化，並將它的一個檢視放入框架版面中。
title: 設定MediaPlay
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 設定MediaPlay {#set-up-the-mediaplayer}

TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可以將其與其他Primetime元件整合。 此外，還提供許多專門設計來最大化視訊播放品質的功能。

將MediaPlayer例項化，並將它的一個檢視放入框架版面中。

1. 具現化 `MediaPlayer`，傳遞 `android.content.Context` 物件至建構函式：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架版面( `android.widget.FrameLayout`)以保留 `ViewGroup` 之 `mediaPlayer`：

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

>此 `MediaPlayer` 例項( `mediaPlayer`)現已可用，且已正確設定為在裝置畫面上顯示視訊內容。
