---
description: 來自TVSDK的事件會指出播放器狀態、發生的錯誤、您請求的動作（例如開始播放的視訊）的完成，或以隱含方式發生的動作（例如廣告完成）。
title: 接聽Primetime播放器事件
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 概述 {#implement-event-listeners-and-callbacks-overview}

事件處理常式可讓TVSDK回應事件。 發生事件時，TVSDK的事件機制會呼叫您註冊的事件處理常式，並將事件資訊傳遞至處理常式。

「Flash執行階段」提供一般事件機制，TVSDK也會使用該機制並定義一系列自訂事件。 您的應用程式必須針對影響您應用程式的TVSDK事件實作事件監聽器。

1. 決定您的應用程式必須監聽的事件。

   * **必要事件**:接聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`MediaPlayerStatusChangeEvent.STATUS_CHANGE`提供播放器狀態，包括錯誤。 任何狀態都可能會影響您播放器的下一步。

   * **其他事件**:選用，視您的應用程式而定。

      例如，如果您將廣告併入播放中，請接聽所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 為每個事件實作事件監聽器。

   TVSDK會將參數值傳回至事件接聽程式回呼。 這些值會提供事件的相關資訊，您可在監聽程式中用於執行適當動作。

   `Event`類列出所有回調介面。 每個介面都會顯示為該介面傳回的參數。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 使用`MediaPlayer.addEventListener`將回呼監聽器註冊到`MediaPlayer`對象。

   `MediaPlayer` 延伸 `flash.events.IEventDispatcher`功能，此功能是Flash播放器核心檔案的一部分，且包含 `addEventListener` 函式和 `removeEventListener`。

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
