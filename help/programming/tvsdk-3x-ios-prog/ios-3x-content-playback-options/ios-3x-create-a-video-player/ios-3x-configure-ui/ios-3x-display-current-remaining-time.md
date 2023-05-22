---
description: 您可以顯示正在播放的內容的當前時間和剩餘時間。
title: 顯示當前時間和剩餘時間
exl-id: f1aebeb7-381b-4bd5-8535-32b902f838d2
source-git-commit: 7e3f1e2dcf855ecd241b2aebc01d9d60c90ed114
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# 顯示當前時間和剩餘時間 {#display-the-current-time-and-remaining-time}

您可以顯示正在播放的內容的當前時間和剩餘時間。

1. 要實現顯示活動內容的當前時間和剩餘時間的顯示，請使用以下示例代碼：

   ```
      // 1. Register for the PTMediaPlayerTimeChangeNotification 
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
        name:PTMediaPlayerTimeChangeNotification object:self.player]; 
   
      ... 
   
      // 2. Create labels for displaying current and remaining time 
      _timeCurrentLabel = [[UILabel alloc] initWithFrame:CGRectMake(50.0, 16.0, 50.0, 21.0)]; 
      _timeCurrentLabel.text = @"00:00:00"; 
      _timeCurrentLabel.font = [UIFont boldSystemFontOfSize:12.0]; 
      _timeCurrentLabel.numberOfLines = 1; 
      _timeCurrentLabel.textAlignment = UITextAlignmentCenter; 
      _timeCurrentLabel.backgroundColor = [UIColor clearColor]; 
      _timeCurrentLabel.textColor =  
        [UIColor colorWithRed:209.0/255.0 green:209.0/255.0 blue:209.0/255.0 alpha:1.0]; 
      [self addSubview:_timeCurrentLabel]; 
   
      _timeRemainingLabel = [[UILabel alloc] initWithFrame:CGRectMake(485.0, 16.0, 50.0, 21.0)]; 
      _timeRemainingLabel.text = @"00:00:00"; 
      _timeRemainingLabel.font = [UIFont boldSystemFontOfSize:12.0]; 
      _timeRemainingLabel.numberOfLines = 1; 
      _timeRemainingLabel.textAlignment = UITextAlignmentCenter; 
      _timeRemainingLabel.backgroundColor = [UIColor clearColor]; 
      _timeRemainingLabel.textColor =  
        [UIColor colorWithRed:209.0/255.0 green:209.0/255.0 blue:209.0/255.0 alpha:1.0]; 
   
      ... 
   
      // 3. This method is called whenever the player time changes  
      (PTMediaPlayerTimeChangeNotification) - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
          //The seekable range provides the playback range of a stream  
          CMTimeRange seekableRange = self.player.seekableRange; 
   
          //Verify if the seekableRange is a valid CMTimeRange  
          if (CMTIMERANGE_IS_VALID(seekableRange)) { 
              double  duration = CMTimeGetSeconds(seekableRange.duration); 
              double currentTime = CMTimeGetSeconds(self.player.currentItem.currentTime);  
              if (CMTIME_IS_INDEFINITE(self.player.currentItem.duration)) { 
                  //If the duration is indefinite then the content is live.  
                  [_timeCurrentLabel setText:[NSString stringWithFormat:@"--:--"]];  
                  [_timeRemainingLabel setText:[NSString stringWithFormat:@"Live"]]; 
              } 
              else { 
                  [_timeCurrentLabel setText:[self timeFormatter:currentTime]];  
                  [_timeRemainingLabel setText:[self timeFormatter:(duration - currentTime)]]; 
              } 
          } 
      } 
   ```

1. 要實現顯示廣告進度和剩餘時間的顯示，請使用以下示例代碼：

   ```
      double adBreakDurationLeft; 
      double adBreakDuration; 
      float currentAdPosition; 
      (void)onMediaPlayerAdBreakStarted:(NSNotification *) notification 
      { 
      PTAdBreak *adBreak = [notification.userInfo objectForKey:PTMediaPlayerAdBreakKey]; 
      self.adBreakDuration = CMTimeGetSeconds(adBreak.range.duration); 
      self.adBreakDurationLeft = self.adBreakDuration; 
      } 
      (void)onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
      { 
      self.adBreakDuration = 0.0f; 
      self.adBreakDurationLeft = 0.0f; 
      } 
      (void)onMediaPlayerAdPlayStarted:(NSNotification *) notification 
      { 
      self.currentAdPosition = 0; 
      } 
      (void)onMediaPlayerAdPlayProgress:(NSNotification *) notification 
      { 
      PTAd *ad = [notification.userInfo objectForKey:PTMediaPlayerAdKey]; 
      CMTime progress = [(NSValue *)[notification.userInfo objectForKey:PTMediaPlayerAdProgressKey] CMTimeValue]; 
      if (ad != nil) { // remaining ad playback time in milliseconds self.currentAdPosition = CMTimeGetSeconds(progress); double timeLeft = self.adBreakDurationLeft - (double)self.currentAdPosition; float currentprogress = 1.0f - (timeLeft/self.adBreakDuration); }  
      } 
      (void)onMediaPlayerAdPlayCompleted:(NSNotification *) notification 
      { 
      PTAd *ad = [notification.userInfo objectForKey:PTMediaPlayerAdKey]; 
      self.adBreakDurationLeft = self.adBreakDurationLeft - ad.primaryAsset.duration; 
      }
   ```

<!--<a id="example_D2FC658F27FC42A0B3E1AEC99B36788B"></a>-->
