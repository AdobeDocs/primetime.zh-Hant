---
description: 當播放到廣告插播、傳遞廣告插播或廣告插播結束時，TVSDK會為目前播放頭的定位定義一些預設行為。
title: 使用廣告自訂播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---


# 使用廣告自訂播放{#customize-playback-with-ads}

當播放到廣告插播、傳遞廣告插播或廣告插播結束時，TVSDK會為目前播放頭的定位定義一些預設行為。

>[!TIP]
>
>您可以使用`PTAdPolicySelector`類別來覆寫預設行為。

預設行為會隨使用者在正常播放期間或在視訊中搜尋時傳遞廣告插播而改變。

您可以透過下列方式自訂廣告播放行為：

* 儲存使用者停止觀看視訊的位置，並在未來作業中在相同位置繼續播放。
* 如果向使用者顯示廣告插播，即使使用者尋求新位置，在數分鐘內不會顯示其他廣告。
* 如果內容在幾分鐘後無法播放，請重新啟動串流，或切換至相同內容的不同來源。

   在容錯播放工作階段中，若要允許使用者略過廣告並繼續到先前的失敗位置，您可以停用前段和／或中段廣告。 TVSDK提供可跳過前段和中段廣告的方法。

## 廣告播放{#section_296ADE00CFEA40CBA1B46142720D13A5}的API元素

TVSDK提供您可用來自訂包含廣告之內容的播放行為的類別和方法。
下列API元素對於自訂播放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>API元素</b></th> 
   <th colname="col2" class="entry"><b>支援廣告的內容</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata  </span> </td> 
   <td colname="col2"> 控制廣告插播是否應標示為已被檢視者觀看，如果是，應於何時標籤。 使用<span class="codeph"> adBreakAsWatched </span>屬性設定並取得監看原則。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector  </span> </td> 
   <td colname="col2"> 允許自訂TVSDK廣告行為的通訊協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> 實作預設TVSDK行為的類別。 您的應用程式可以覆寫此類別，以自訂預設行為，而不需實作完整的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer  </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>。 <p>這是播放的本機時間，排除已置入的廣告插播。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> 。 <p>在此，搜索相對於流中的本地時間發生。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>。 <p>時間軸上的虛擬位置會轉換為本機位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak  </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched屬 </span> 性。指出檢視者是否已觀看廣告。 </td> 
  </tr> 
 </tbody> 
</table>

## 設定自訂播放{#section_8209BAACC7814C9399988DC7DE9CF4CA}

在自訂或覆寫廣告行為之前，請先向TVSDK註冊廣告政策例項。

若要自訂廣告行為，請執行下列其中一項作業：

* 遵循`PTAdPolicySelector`協定並實施所有必需的策略選擇方法。

   如果您需要覆寫&#x200B;**all**&#x200B;預設廣告行為，建議使用此選項。

* 覆寫`PTDefaultAdPolicySelector`類別，並僅提供需要自訂的行為的實施。

   如果您只需要覆寫預設行為的&#x200B;**some**，建議使用此選項。

對於這兩個選項，請完成下列任務：

1. 透過用戶端工廠註冊TVSDK要使用的原則例項。

   >[!NOTE]
   >
   >取消分配`PTMediaPlayer`實例時，會清除在播放開始時註冊的自定義廣告策略。 每次建立新的播放作業時，您的應用程式都必須註冊原則選擇器例項。

   例如：

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 實作您的自訂。

## 在{#section_99809BE4D9BB4DEEBBF596C746CA428A}期間略過廣告插播

依預設，當使用者搜尋廣告插播時，TVSDK會強制播放廣告插播。 如果從先前的中斷完成所經過的時間在特定分鐘內，您可以自訂跳過廣告中斷的行為。

>[!IMPORTANT]
>
>當有內部搜尋要略過廣告時，可能會在播放中稍微暫停。

下列自訂廣告政策選擇器範例會在使用者觀看廣告插播後的5分鐘（塗鴉牆時鐘時間）跳過廣告。

1. 透過用戶端工廠註冊TVSDK要使用的原則例項。

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 實作您的自訂。

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## 儲存視訊位置並稍後繼續{#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。

動態插入的廣告在使用者工作階段間不同，因此將位置&#x200B;**與**&#x200B;接合的廣告儲存，是指未來工作階段中的不同位置。 TVSDK提供在忽略拼接廣告時擷取播放位置的方法。

1. 當使用者結束視訊時，您的應用程式會擷取並儲存視訊中的位置。

   >[!TIP]
   >
   >廣告期間不包含在內。

   由於廣告模式、頻率上限設定等原因，每個工作階段的廣告插播都會有所不同。 視訊在某個作業中的目前時間在未來作業中可能不同。 在視訊中儲存位置時，應用程式會擷取本機時間。 使用`localTime`屬性讀取此位置，您可將此位置保存在設備上或伺服器上的資料庫中。

   例如，如果使用者是視訊的第20分鐘，而此位置包含5分鐘廣告，則`currentTime`將是1200秒，而此位置的`localTime`將是900秒。

   >[!IMPORTANT]
   >
   >即時／線性串流的本機時間與目前時間相同。 在這種情況下，`convertToLocalTime`沒有作用。 對於VOD，當廣告播放時，當地時間保持不變。

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. 若要在先前作業儲存的相同位置繼續視訊，請使用`seekToLocalTime`。

   >[!TIP]
   >
   >此方法僅與本機時間值一起呼叫。 如果以目前的時間結果呼叫方法，就會發生錯誤行為。

   要查找當前時間，請使用`seekToTime`。

1. 當您的應用程式收到`PTMediaPlayerStatusReady`狀態變更事件時，請尋找儲存的本機時間。

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 依照廣告原則介面中的指定，提供廣告分段。
1. 延伸預設廣告原則選擇器，以實作自訂廣告原則選擇器。
1. 透過實作`selectAdBreaksToPlay`，提供必須向使用者顯示的廣告插播

   >[!NOTE]
   >
   >此方法包括前段廣告插播和中段廣告插播，前段廣告插播於本機時間位置。 您的應用程式可決定播放前段廣告插播並繼續到指定的當地時間、播放中段廣告插播並繼續到指定的當地時間，或不播放廣告插播。