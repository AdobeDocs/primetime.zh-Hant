---
description: 您可以顯示正在播放之內容的目前和剩餘時間。
title: 顯示目前時間和剩餘時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# 顯示目前時間和剩餘時間 {#display-the-current-time-and-remaining-time}

您可以顯示正在播放之內容的目前和剩餘時間。

1. 若要實作顯示使用中內容目前和剩餘時間的顯示，請使用下列範常式式碼：

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

1. 若要實作顯示廣告進度和剩餘時間的顯示，請使用下列範常式式碼：

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
