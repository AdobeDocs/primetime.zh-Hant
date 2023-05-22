---
description: TVSDK提供用於建立高級視頻播放器應用程式（您的Mighide播放器）的工具，您可以與其他Mighide元件整合。 它還提供了多種功能，旨在最大限度地提高視頻播放的質量。
title: 設定媒體播放器
exl-id: 99fdc4c1-0c67-4de5-87a5-b42d76f43ae9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 設定媒體播放器 {#set-up-the-media-player}

TVSDK提供用於建立高級視頻播放器應用程式（您的Mighide播放器）的工具，您可以與其他Mighide元件整合。 它還提供了多種功能，旨在最大限度地提高視頻播放的質量。

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

實例化 `MediaPlayer` 並將其視圖放入框架佈局中。

1. 實例化 `MediaPlayer`，通過 `android.content.Context` 對象到建構子：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架佈局( `android.widget.FrameLayout`) `ViewGroup` 共 `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >下面是要建立的代碼段 `_viewGroup`。

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

   >[!NOTE]
   >
   >的 `MediaPlayer` 實例( `mediaPlayer`)現在可用，並且已正確配置以在設備螢幕上顯示視頻內容。
