---
description: 當播放達到廣告插播、通過廣告插播或結束廣告插播時，TVSDK會為目前播放點的位置定義一些預設行為。
title: 使用廣告自訂播放
exl-id: f59e94c2-7ca0-4e0b-b0b1-af076fdd4064
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 使用廣告自訂播放{#customize-playback-with-ads}

當播放達到廣告插播、通過廣告插播或結束廣告插播時，TVSDK會為目前播放點的位置定義一些預設行為。

>[!TIP]
>
>您可以使用來覆寫預設行為 `PTAdPolicySelector` 類別。

預設行為會有所不同，具體取決於使用者是在正常播放期間或透過在視訊中搜尋而經過廣告插播。

您可以透過下列方式自訂廣告播放行為：

* 儲存使用者停止觀看視訊的位置，並在未來工作階段的相同位置繼續播放。
* 如果向使用者呈現廣告插播，在幾分鐘內不會顯示其他廣告，即使使用者尋求新位置。
* 如果內容在幾分鐘後無法播放，請重新啟動串流或容錯移轉至相同內容的不同來源。

   在容錯移轉播放工作階段上，若要允許使用者略過廣告並繼續前往上一個失敗位置，您可以停用前段和/或中段廣告。 TVSDK提供可讓您略過前段和中段廣告的方法。

## 廣告播放的API元素 {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK提供類別和方法，讓您用來自訂包含廣告之內容的播放行為。
下列API元素對於自訂播放很實用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支援廣告的內容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> 控制廣告插播是否應該標示為已被檢視者觀看，如果是，何時標示為。 使用設定並取得追蹤原則 <span class="codeph"> adBreakAsWatched </span> 屬性。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ptadPolicySelector </span> </td> 
   <td colname="col2"> 允許自訂TVSDK廣告行為的通訊協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 實作預設TVSDK行為的類別。 您的應用程式可以覆寫此類別來自訂預設行為，而無需實作完整的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>這是播放的當地時間，不包括置入的廣告插播。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>在此處，搜尋會相對於資料流中的當地時間進行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>時間軸上的虛擬位置會轉換為本機位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> iswatched </span> 屬性。 指出檢視器是否觀看過廣告。 </td> 
  </tr> 
 </tbody> 
</table>

## 設定自訂播放 {#section_8209BAACC7814C9399988DC7DE9CF4CA}

在您可以自訂或覆寫廣告行為之前，請先使用TVSDK註冊廣告原則執行個體。

若要自訂廣告行為，請執行下列任一項作業：

* 符合 `PTAdPolicySelector` 通訊協定，並實作所有必要的原則選取方法。

   如果您需要覆寫，建議使用此選項 **全部** 預設廣告行為。

* 覆寫 `PTDefaultAdPolicySelector` 類別並提供僅用於需要自訂之行為的實作。

   如果您只需要覆寫，則建議使用此選項 **部分** 預設行為的ID。

針對這兩個選項，請完成下列工作：

1. 透過使用者端處理站註冊TVSDK要使用的原則執行個體。

   >[!NOTE]
   >
   >播放開始時註冊的自訂廣告原則會在以下情況下清除： `PTMediaPlayer` 執行個體已取消配置。 您的應用程式必須在每次建立新播放工作階段時註冊原則選擇器執行個體。

   例如：

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 實作您的自訂。

## 略過一段時間的廣告插播 {#section_99809BE4D9BB4DEEBBF596C746CA428A}

依預設，當使用者搜尋廣告插播時，TVSDK會強製播放廣告插播。 如果從前一個插播完成經過的時間是在特定分鐘數內，您可以自訂略過廣告插播的行為。

>[!IMPORTANT]
>
>當有要略過廣告的內部搜尋時，播放中可能會稍微暫停。

以下自訂廣告原則選擇器的範例會在使用者觀看廣告插播後5分鐘（牆上時鐘時間）內略過廣告。

1. 透過使用者端處理站註冊TVSDK要使用的原則執行個體。

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

## 儲存視訊位置並稍後繼續 {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

您可以將目前的播放位置儲存在視訊中，並在未來工作階段的相同位置繼續播放。

動態插入的廣告會因使用者工作階段而異，所以儲存位置 **替換為** 拼接廣告是指未來工作階段中的不同位置。 TVSDK提供在忽略拼接廣告時擷取播放位置的方法。

1. 當使用者結束視訊時，您的應用程式會擷取並儲存視訊中的位置。

   >[!TIP]
   >
   >不包括廣告持續時間。

   由於廣告模式、頻率上限等原因，每個工作階段的廣告插播可能會有所不同。 一個工作階段中視訊的目前時間，可能會與未來工作階段中的不同。 在視訊中儲存位置時，應用程式會擷取當地時間。 使用  `localTime` 屬性來讀取此位置，您可以將其儲存在裝置上或伺服器的資料庫中。

   例如，如果使用者在影片的第20分鐘，而此位置包含五分鐘的廣告， `currentTime` 將會是1200秒，而 `localTime` 在此位置將為900秒。

   >[!IMPORTANT]
   >
   >即時/線性資料流的當地時間和目前時間相同。 在這種情況下， `convertToLocalTime` 沒有效果。 對於VOD，播放廣告時當地時間保持不變。

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

1. 若要在相同位置繼續播放視訊：若要從先前工作階段儲存的位置繼續播放視訊，請使用 `seekToLocalTime`

   >[!TIP]
   >
   >此方法只會以本機時間值呼叫。 如果使用目前時間結果呼叫方法，則會發生錯誤行為。

   若要搜尋到目前時間，請使用 `seekToTime`.

1. 當您的應用程式收到 `PTMediaPlayerStatusReady` 狀態變更事件，搜尋已儲存的當地時間。

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 提供廣告原則介面中指定的廣告插播。
1. 擴充預設廣告原則選擇器，實作自訂廣告原則選擇器。
1. 透過實作，提供必須呈現給使用者的廣告插播 `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >此方法包括前段廣告插播和當地時間位置之前的中段廣告插播。 您的應用程式可以決定播放前段廣告插播並繼續到指定的當地時間、播放中段廣告插播並繼續到指定的當地時間，或不播放任何廣告插播。
