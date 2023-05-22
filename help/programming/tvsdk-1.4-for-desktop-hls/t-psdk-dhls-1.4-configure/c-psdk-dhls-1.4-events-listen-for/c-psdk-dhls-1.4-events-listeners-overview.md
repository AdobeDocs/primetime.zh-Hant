---
description: TVSDK中的事件指示播放器的狀態、發生的錯誤、您請求的操作（如視頻開始播放）的完成或隱式發生的操作（如廣告完成）。
title: 收聽黃金時段播放機活動
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 概述 {#implement-event-listeners-and-callbacks-overview}

事件處理程式允許TVSDK響應事件。 當發生事件時，TVSDK的事件機制將調用您註冊的事件處理程式並將事件資訊傳遞給處理程式。

Flash運行時提供一種通用事件機制，TVSDK也使用該機制並定義一系列自定義事件。 您的應用程式必須為影響您的應用程式的TVSDK事件實現事件偵聽器。

1. 確定應用程式必須偵聽哪些事件。

   * **必需事件**:收聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `MediaPlayerStatusChangeEvent.STATUS_CHANGE` 提供播放器狀態，包括錯誤。 任何狀態都可能影響玩家的下一步。

   * **其他事件**:可選，具體取決於您的應用程式。

      例如，如果在播放中加入廣告，請傾聽所有 `AdBreakPlaybackEvent` 和 `AdPlaybackEvent` 事件。

1. 為每個事件實現事件偵聽器。

   TVSDK將參數值返回到事件監聽器回調。 這些值提供了有關事件的相關資訊，您可以在監聽器中使用這些事件執行相應的操作。

   的 `Event` 類列出所有回調介面。 每個介面都顯示為該介面返回的參數。

   例如：

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. 將回調偵聽器註冊到 `MediaPlayer` 對象使用 `MediaPlayer.addEventListener`。

   `MediaPlayer` 延伸 `flash.events.IEventDispatcher`，它是Flash播放器核心檔案的一部分，包括功能 `addEventListener` 和 `removeEventListener`。

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
