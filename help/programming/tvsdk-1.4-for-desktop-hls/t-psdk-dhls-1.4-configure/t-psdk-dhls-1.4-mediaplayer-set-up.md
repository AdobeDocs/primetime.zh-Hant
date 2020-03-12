---
description: MediaPlayer介面可封裝媒體播放器的功能與行為。
seo-description: MediaPlayer介面可封裝媒體播放器的功能與行為。
seo-title: 設定MediaPlayer
title: 設定MediaPlayer
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 設定MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），您可將它與其他Primetime元件整合。

使用您平台的工具來建立播放器，並將它連接至TVSDK中的媒體播放器檢視，TVSDK提供播放和管理視訊的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定按鈕來呼叫這些TVSDK方法。MediaPlayer介面封裝媒體播放器的功能與行為。

TVSDK提供單一介面實 `MediaPlayer` 作：defaultMediaPlayer類別。 當您需要視訊播放功能時，請執行個體化 `DefaultMediaPlayer`。

>[!NOTE]
>
>僅與介 `DefaultMediaPlayer` 面公開的方法互動實 `MediaPlayer` 例。

1. 使用應用 `MediaPlayerContext` 程式載入的例項 `authorizedFeatures` 實例化(請 [參閱載入已簽署的Token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md))。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 使用公 `MediaPlayer` 用建立工廠方法實例化，傳遞上下文 `MediaPlayerContext` 物件：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   這會傳回一般 `MediaPlayer` 介面。 1.執行個 `MediaPlayerView` 體化並指定要使用的StageVideo執行個體：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 將實例 `MediaPlayerView` 與新建立的視圖關聯：

   ```
   mediaPlayer.view = view;
   ```

1. 將執 `MediaPlayerView` 行個體置於裝置的螢幕上：

   ```
   container.addChild(view)
   ```

現在 `MediaPlayer` 可使用此例項，並正確設定以在裝置螢幕上顯示視訊內容。