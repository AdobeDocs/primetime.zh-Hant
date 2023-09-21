---
description: PTMmediaPlayer介面會封裝媒體播放器物件的功能和行為。
title: 設定PTMediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 設定PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可以將其與其他Primetime元件整合。

使用平台的工具來建立播放器，並將其連線至TVSDK中的媒體播放器檢視，該檢視具有播放和管理視訊的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定呼叫這些TVSDK方法的按鈕。

PTMmediaPlayer介面會封裝媒體播放器物件的功能和行為。

若要設定您的 `PTMediaPlayer`：

1. 從您的使用者介面擷取媒體的URL，例如在文字欄位中。

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 建立 `PTMetadata`.

   假設您的方法 `createMetada` 準備中繼資料(請參閱 [Advertising](../../ios-3x-advertising/ios-3x-advertising-requirements.md))。

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 建立 `PTMediaPlayerItem` 透過使用您的 `PTMetadata` 執行個體。

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. 將觀察者新增至TVSDK傳送的通知。

   ```
   [self addObservers]
   ```

1. 建立 `PTMediaPlayer` 使用您的新的 `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 在播放器上設定屬性。

   以下是一些可用的 `PTMediaPlayer` 屬性：

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. 設定播放器的檢視屬性。

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. 在目前檢視的子檢視中新增播放器的檢視。

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 呼叫 `play` 以開始播放媒體。

   ```
   [player play];
   ```
