---
description: 當播放達到廣告中斷、通過廣告中斷或以廣告中斷結束時，TVSDK定義一些用於定位當前播放頭的預設行為。
title: 使用廣告自定義播放
exl-id: f59e94c2-7ca0-4e0b-b0b1-af076fdd4064
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 使用廣告自定義播放{#customize-playback-with-ads}

當播放達到廣告中斷、通過廣告中斷或以廣告中斷結束時，TVSDK定義一些用於定位當前播放頭的預設行為。

>[!TIP]
>
>可以使用 `PTAdPolicySelector` 類。

預設行為會因用戶在正常播放期間還是通過在視頻中查找而不同。

可以通過以下方式自定義廣告播放行為：

* 保存用戶停止觀看視頻的位置，並在將來會話中在同一位置繼續播放。
* 如果向用戶呈現廣告中斷，則即使用戶尋找新位置，也不顯示附加廣告數分鐘。
* 如果內容在幾分鐘後無法播放，請重新啟動流或故障轉移到同一內容的其他源。

   在故障切換回放會話中，為了允許用戶跳過廣告並恢復到上一個失敗位置，可以禁用前滾和/或中滾廣告。 TVSDK提供了跳過預卷廣告和中卷廣告的方法。

## 用於廣告播放的API元素 {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK提供可用於自定義包含廣告的內容的播放行為的類和方法。
以下API元素對自定義回放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支援廣告的內容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAd元資料 </span> </td> 
   <td colname="col2"> 控制廣告分段是否應被標籤為已被觀眾觀看，如果是，何時標籤。 使用設定和獲取監視策略 <span class="codeph"> adBreakAsStated </span> 屬性。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> 允許自定義TVSDK廣告行為的協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 實現預設TVSDK行為的類。 您的應用程式可以覆蓋此類，以自定義預設行為而不實施完整的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> 本地時間 </span>。 <p>這是回放的本地時間，不包括放置的廣告分段。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> 。 <p>此處，查找相對於流中的本地時間發生。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>。 <p>時間線上的虛擬位置被轉換為本地位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> 已監視 </span> 屬性。 指示查看者是否已觀看廣告。 </td> 
  </tr> 
 </tbody> 
</table>

## 設定自定義播放 {#section_8209BAACC7814C9399988DC7DE9CF4CA}

在可以自定義或覆蓋廣告行為之前，請向TVSDK註冊廣告策略實例。

要自定義廣告行為，請執行以下操作之一：

* 符合 `PTAdPolicySelector` 協定和實現所有所需的策略選擇方法。

   如果需要覆蓋，建議使用此選項 **全部** 預設廣告行為。

* 覆蓋 `PTDefaultAdPolicySelector` 類並僅為那些需要自定義的行為提供實現。

   如果僅需要覆蓋，建議使用此選項 **有** 的子菜單。

對於這兩個選項，請完成以下任務：

1. 通過客戶端工廠註冊TVSDK要使用的策略實例。

   >[!NOTE]
   >
   >在播放開始時註冊的自定義廣告策略在 `PTMediaPlayer` 實例被取消分配。 每次建立新的回放會話時，應用程式都必須註冊策略選擇器實例。

   例如：

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 實施您的自定義。

## 跳過一段時間的廣告中斷 {#section_99809BE4D9BB4DEEBBF596C746CA428A}

預設情況下，當用戶搜索廣告時，TVSDK強制播放廣告。 如果從上一個中斷完成所經過的時間在特定分鐘數內，則可以自定義跳過廣告中斷的行為。

>[!IMPORTANT]
>
>當內部尋道要跳過廣告時，回放可能會稍稍停頓。

以下自定義廣告策略選擇器的示例在用戶觀看廣告中斷後的5分鐘（掛鐘時間）內跳過廣告。

1. 通過客戶端工廠註冊TVSDK要使用的策略實例。

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 實施您的自定義。

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

## 保存視頻位置，稍後繼續 {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

您可以保存視頻中的當前播放位置，並在將來的會話中在相同位置繼續播放。

動態插入的廣告在用戶會話之間不同，因此保存位置 **與** 拼接廣告是指將來會話中的不同位置。 TVSDK提供了在忽略拼接廣告時檢索回放位置的方法。

1. 當用戶退出視頻時，應用程式將檢索並保存視頻中的位置。

   >[!TIP]
   >
   >不包括廣告持續時間。

   由於廣告模式、頻率封頂等原因，廣告中斷在每個會話中都可能會有所不同。 視頻在一個會話中的當前時間在未來會話中可能不同。 當在視頻中保存位置時，應用程式檢索本地時間。 使用  `localTime` 用於讀取此位置的屬性，您可以將此位置保存在設備上或伺服器上的資料庫中。

   例如，如果用戶在視頻的第20分鐘，而此位置包含5分鐘的廣告， `currentTime` 1200秒，而 `localTime` 這個位置是900秒。

   >[!IMPORTANT]
   >
   >即時/線性流的本地時間和當前時間相同。 在這個例子中， `convertToLocalTime` 沒有效果。 對於視頻點播，在播放廣告時，本地時間保持不變。

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

1. 要在同一位置恢復視頻：要從上次會話中保存的位置繼續播放視頻，請使用 `seekToLocalTime`

   >[!TIP]
   >
   >此方法僅使用本地時間值調用。 如果使用當前時間結果調用方法，則會發生錯誤行為。

   要查找當前時間，請使用 `seekToTime`。

1. 當您的應用程式收到 `PTMediaPlayerStatusReady` 狀態更改事件，查找已保存的本地時間。

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 提供在廣告策略介面中指定的廣告分段。
1. 通過擴展預設廣告策略選擇器來實現自定義廣告策略選擇器。
1. 通過實現，提供必須向用戶顯示的廣告分段 `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >該方法包括在局部時間位置之前的預卷和中卷和斷點。 您的應用程式可以決定播放預播廣告中斷，然後繼續到指定的本地時間，播放中播廣告中斷，然後繼續到指定的本地時間，或者不播放廣告中斷。
