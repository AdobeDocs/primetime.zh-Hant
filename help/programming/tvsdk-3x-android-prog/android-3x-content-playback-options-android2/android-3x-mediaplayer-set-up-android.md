---
description: TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），讓您可與其他Primetime元件整合。 此外，它還提供多種功能，可讓視訊播放品質發揮最大。
seo-description: TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），讓您可與其他Primetime元件整合。 此外，它還提供多種功能，可讓視訊播放品質發揮最大。
seo-title: 設定媒體播放器
title: 設定媒體播放器
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 設定媒體播放器 {#set-up-the-media-player}

TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），讓您可與其他Primetime元件整合。 此外，它還提供多種功能，可讓視訊播放品質發揮最大。

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

執行個 `MediaPlayer` 體化並將檢視置入影格版面。

1. 實例 `MediaPlayer`化，將對象 `android.content.Context` 傳遞到建構子：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供影格版面( `android.widget.FrameLayout`)，以容納 `ViewGroup` 下列 `mediaPlayer`項目：

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >以下是要建立的程式碼片段 `_viewGroup`。

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 在影格版面 `mediaPlayer` 內放置檢視：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >現在 `MediaPlayer` 可使用實 `mediaPlayer`例()，並正確設定以在裝置螢幕上顯示視訊內容。