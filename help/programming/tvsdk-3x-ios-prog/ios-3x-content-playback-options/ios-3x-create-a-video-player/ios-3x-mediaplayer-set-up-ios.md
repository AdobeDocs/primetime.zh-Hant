---
description: PTMediaPlayer介面可封裝媒體播放器物件的功能與行為。
seo-description: PTMediaPlayer介面可封裝媒體播放器物件的功能與行為。
seo-title: 設定PTMediaPlayer
title: 設定PTMediaPlayer
uuid: 698034d3-1260-416f-83b0-6b7d058750a0
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 設定PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK提供工具來建立進階視訊播放器應用程式（您的Primetime播放器），您可將它與其他Primetime元件整合。

使用您平台的工具來建立播放器，並將它連接至TVSDK中的媒體播放器檢視，TVSDK提供播放和管理視訊的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定按鈕來呼叫這些TVSDK方法。

PTMediaPlayer介面可封裝媒體播放器物件的功能與行為。

要設定`PTMediaPlayer`:

1. 從使用者介面擷取媒體的URL，例如在文字欄位中。

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 建立`PTMetadata`。

   假設您的方法`createMetada`準備中繼資料（請參閱[ Advertising](../../ios-3x-advertising/ios-3x-advertising-requirements.md)）。

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 使用您的`PTMetadata`實例建立`PTMediaPlayerItem`。

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. 新增觀察者至TVSDK所派送的通知。

   ```
   [self addObservers]
   ```

1. 使用新的`PTMediaPlayerItem`建立`PTMediaPlayer`。

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 在您的播放器上設定屬性。

   以下是一些可用的`PTMediaPlayer`屬性：

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

1. 呼叫`play`以開始媒體播放。

   ```
   [player play];
   ```
