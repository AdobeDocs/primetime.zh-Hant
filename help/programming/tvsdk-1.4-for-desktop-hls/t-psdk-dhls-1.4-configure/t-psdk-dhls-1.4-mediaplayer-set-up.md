---
description: MediaPlayer介面會封裝媒體播放器的功能和行為。
title: 設定MediaPlay
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 設定MediaPlay {#set-up-the-mediaplayer}

TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可以將其與其他Primetime元件整合。

使用平台的工具來建立播放器，並將其連線至TVSDK中的媒體播放器檢視，該檢視具有播放和管理視訊的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定按鈕以呼叫這些TVSDK方法。MediaPlayer介面會封裝媒體播放器的功能和行為。

TVSDK提供 `MediaPlayer` 介面： DefaultMediaPlayer類別。 當您需要視訊播放功能時，請具現化 `DefaultMediaPlayer`.

>[!NOTE]
>
>與 `DefaultMediaPlayer` 執行個體只能使用下列專案公開的方法： `MediaPlayer` 介面。

1. 例項化 `MediaPlayerContext` 使用已載入的應用程式 `authorizedFeatures` 執行個體(請參閱 [載入您的簽署Token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md))。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 例項化 `MediaPlayer` 使用public create factory方法，傳遞 `MediaPlayerContext` 內容物件：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   這會傳回泛型 `MediaPlayer` 介面。 1.例項化 `MediaPlayerView` 並指定要使用的StageVideo例項：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 建立關聯 `MediaPlayerView` 具有新建立檢視的例項：

   ```
   mediaPlayer.view = view;
   ```

1. 放置 `MediaPlayerView` 裝置熒幕上的執行個體：

   ```
   container.addChild(view)
   ```

此 `MediaPlayer` 執行個體現在可供使用，並已正確設定為在裝置畫面上顯示視訊內容。
