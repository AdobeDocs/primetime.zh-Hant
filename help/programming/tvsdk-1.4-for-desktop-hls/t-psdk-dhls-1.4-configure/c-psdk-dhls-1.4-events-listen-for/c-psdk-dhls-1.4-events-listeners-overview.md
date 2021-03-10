---
description: 來自TVSDK的事件會指出播放器的狀態、發生的錯誤、您所要求的動作的完成，例如視訊開始播放，或是隱含發生的動作，例如廣告完成。
title: 監聽Primetime Player活動
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 概述{#implement-event-listeners-and-callbacks-overview}

事件處理常式可讓TVSDK回應事件。 發生事件時，TVSDK的事件機制會呼叫您已註冊的事件處理常式，並將事件資訊傳遞給處理常式。

「Flash執行時期」提供一般事件機制，TVSDK也會使用並定義一系列自訂事件。 您的應用程式必須針對影響您應用程式的TVSDK事件實作事件接聽程式。

如需視訊分析事件的完整清單，請參閱[追蹤核心視訊播放](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html)。

1. 決定您的應用程式必須監聽哪些事件。

   * **必要事件**:監聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`MediaPlayerStatusChangeEvent.STATUS_CHANGE`提供播放器狀態，包括錯誤。 任何狀態都可能會影響您播放器的下一步。

   * **其他事件**:可選，視您的應用程式而定。

      例如，如果您在播放中加入廣告，請監聽所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 為每個事件實施事件偵聽器。

   TVSDK會將參數值傳回至您的事件接聽程式回呼。 這些值會提供有關事件的相關資訊，您可在監聽程式中用來執行適當動作。

   `Event`類列出所有回調介面。 每個介面都會顯示該介面傳回的參數。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 使用`MediaPlayer.addEventListener`將回呼偵聽器註冊到`MediaPlayer`對象。

   `MediaPlayer` extends, `flash.events.IEventDispatcher`它是Flash播放器核心檔案的一部分，並包含函 `addEventListener` 數和 `removeEventListener`。

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


