---
description: MediaPlayer介面可封裝媒體播放器的功能與行為。
title: 設定MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 設定MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），您可將它與其他Primetime元件整合。

使用您平台的工具來建立播放器，並將它連接至TVSDK中的媒體播放器檢視，TVSDK提供播放和管理視訊的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定按鈕來呼叫這些TVSDK方法。MediaPlayer介面封裝媒體播放器的功能與行為。

TVSDK提供`MediaPlayer`介面的單一實作：defaultMediaPlayer類別。 當您需要視訊播放功能時，請執行個體化`DefaultMediaPlayer`。

>[!NOTE]
>
>僅與`MediaPlayer`介面公開的方法交互。`DefaultMediaPlayer`

1. 使用應用程式載入的`authorizedFeatures`例項實例化`MediaPlayerContext`（請參閱[載入您的已簽署Token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)）。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 使用public create factory方法實例化`MediaPlayer`，傳遞`MediaPlayerContext`上下文對象：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   這會傳回一般`MediaPlayer`介面。 1.實例化`MediaPlayerView`並指定要使用的StageVideo實例：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 將`MediaPlayerView`實例與新建立的視圖關聯：

   ```
   mediaPlayer.view = view;
   ```

1. 將`MediaPlayerView`實例置於設備的螢幕上：

   ```
   container.addChild(view)
   ```

`MediaPlayer`例項現已可用，並已正確設定，可在裝置螢幕上顯示視訊內容。