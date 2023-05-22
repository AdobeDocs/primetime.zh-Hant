---
description: PTMediaPlayer介面封裝媒體播放器對象的功能和行為。
title: 設定PTMediaPlayer
exl-id: cf8f46c8-c52a-4f44-b493-965ce1b50c68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 設定PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK提供用於建立高級視頻播放器應用程式（您的Mighide播放器）的工具，您可以將其與其他Mighide元件整合。

使用平台的工具建立播放器並將其連接到TVSDK中的媒體播放器視圖，TVSDK具有播放和管理視頻的方法。 例如，TVSDK提供播放和暫停方法。 您可以在平台上建立用戶介面按鈕，並設定按鈕以調用這些TVSDK方法。

PTMediaPlayer介面封裝媒體播放器對象的功能和行為。

設定 `PTMediaPlayer`:

1. 從用戶介面獲取媒體的URL，例如，在文本欄位中。

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 建立 `PTMetadata`。

   假設您的方法 `createMetada` 準備元資料（請參見） [廣告](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md))。

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 建立 `PTMediaPlayerItem` 使用 `PTMetadata` 實例。

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. 向TVSDK調度的通知添加觀察員。

   ```
   [self addObservers]
   ```

1. 建立 `PTMediaPlayer` 使用新 `PTMediaPlayerItem`。

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 設定播放器的屬性。

   以下是一些可用 `PTMediaPlayer` 屬性：

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. 設定播放器的視圖屬性。

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. 在當前視圖的子視圖中添加播放器的視圖。

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 呼叫 `play` 啟動媒體播放。

   ```
   [player play];
   ```
