---
description: MediaPlayer介面封裝媒體播放器的功能和行為。
title: 設定MediaPlayer
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 設定MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供用於建立高級視頻播放器應用程式（您的Mighide播放器）的工具，您可以將其與其他Mighide元件整合。

使用平台的工具建立播放器並將其連接到TVSDK中的媒體播放器視圖，TVSDK具有播放和管理視頻的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立用戶介面按鈕並設定按鈕以調用這些TVSDK方法。MediaPlayer介面封裝媒體播放器的功能和行為。

TVSDK提供了 `MediaPlayer` 介面：DefaultMediaPlayer類。 當需要視頻播放功能時，實例化 `DefaultMediaPlayer`。

>[!NOTE]
>
>與 `DefaultMediaPlayer` 僅使用 `MediaPlayer` 。

1. 實例化 `MediaPlayerContext` 使用應用程式載入 `authorizedFeatures` 實例(請參閱 [載入簽名標籤](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md))。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 實例化 `MediaPlayer` 使用公共建立工廠方法，傳遞 `MediaPlayerContext` 上下文對象：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   這返回泛型 `MediaPlayer` 。 1。實例化 `MediaPlayerView` 並指定要使用的StageVideo實例：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 關聯 `MediaPlayerView` 具有新建立視圖的實例：

   ```
   mediaPlayer.view = view;
   ```

1. 放置 `MediaPlayerView` 設備螢幕上的實例：

   ```
   container.addChild(view)
   ```

的 `MediaPlayer` 實例現在可用，並且已正確配置為在設備螢幕上顯示視頻內容。
