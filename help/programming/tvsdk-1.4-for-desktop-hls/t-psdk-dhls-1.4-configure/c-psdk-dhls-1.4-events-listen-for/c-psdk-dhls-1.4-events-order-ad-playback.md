---
description: 當您的播放包含廣告時，TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。
seo-description: 當您的播放包含廣告時，TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。
seo-title: 廣告活動順序
title: 廣告活動順序
uuid: 34a6a606-2f2e-42de-88fd-c91202cafddf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 廣告活動順序{#order-of-advertising-events}

當您的播放包含廣告時，TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

播放廣告時，事件的順序為：

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* 廣告插播中的每個廣告都會傳送下列訊息：

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` （在廣告播放期間多次）
   * `AdClickEvent.AD_CLICK` （每次點按時）
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

下列範例顯示廣告播放事件的典型進展：

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 
```

