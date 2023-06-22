---
description: 來自TVSDK的事件會指出播放器的狀態、發生的錯誤、您已要求的動作（例如開始播放的視訊）的完成，或是隱含發生的動作（例如廣告完成）。
title: 接聽Primetime播放器事件
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 概觀 {#implement-event-listeners-and-callbacks-overview}

事件處理常式可讓TVSDK回應事件。 當事件發生時，TVSDK的事件機制會呼叫您註冊的事件處理常式，並將事件資訊傳遞給處理常式。

Flash執行階段提供了一般事件機制，TVSDK也會使用並定義一系列自訂事件。 您的應用程式必須為影響您應用程式的TVSDK事件實作事件接聽程式。

1. 判斷應用程式必須監聽的事件。

   * **必要事件**：接聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `MediaPlayerStatusChangeEvent.STATUS_CHANGE` 提供播放器狀態，包括錯誤。 任何狀態都可能影響您的播放器的下一步。

   * **其他事件**：選擇性，視您的應用程式而定。

      例如，如果您在播放中加入廣告，請聆聽所有內容 `AdBreakPlaybackEvent` 和 `AdPlaybackEvent` 事件。

1. 實作每個事件的事件接聽程式。

   TVSDK會傳回事件接聽程式回呼的引數值。 這些值會提供有關事件的相關資訊，您可在接聽程式中用來執行適當的動作。

   此 `Event` class會列出所有回呼介面。 每個介面都會顯示該介面傳回的引數。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 向註冊回呼接聽程式 `MediaPlayer` 物件，使用 `MediaPlayer.addEventListener`.

   `MediaPlayer` 延伸 `flash.events.IEventDispatcher`，是Flash播放器核心檔案的一部分，包含函式 `addEventListener` 和 `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
