---
description: 事件處理常式可讓您回應TVSDK事件。
title: 實作事件偵聽器和回呼
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# 實施事件偵聽器和回呼{#implement-event-listeners-and-callbacks}

事件處理常式可讓您回應TVSDK事件。

發生事件時，TVSDK的事件機制會呼叫您已註冊的事件處理常式，並傳遞事件資訊。

TVSDK將監聽器定義為`MediaPlayer`介面內的公用內部介面。

您的應用程式必須針對任何影響您應用程式的TVSDK事件實作事件接聽程式。

1. 決定您的應用程式必須監聽的事件。

   * 必要事件：監聽所有播放事件。

      >[!IMPORTANT]
      >
      >監聽狀態變更事件，當玩家的狀態變更時，您需要知道。 它提供的資訊包含可能影響播放器下一步動作的錯誤。

   * 如需其他事件，請視您的應用程式而定，參閱events-summary。

1. 為每個事件實作並新增事件監聽器。

   >[!NOTE]
   >
   >對於大多數事件，TVSDK會將引數傳遞給事件監聽器。 這些值提供事件的相關資訊，可協助您決定下一步要做什麼。 `MediaPlayerEvent`枚舉列出了`MediaPlayer`調度的所有事件。 如需詳細資訊，請參閱events-summary。

   例如，如果`mPlayer`是`MediaPlayer`的實例，則以下是如何添加和構建事件偵聽器：

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## 播放事件的順序{#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

下列範例顯示播放期間發生的某些事件的順序。

通過`MediaPlayer.replaceCurrentResource`成功載入媒體資源時，事件順序為：

1. `MediaPlayerEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>在主線程上載入媒體資源。 如果在後台線程上載入媒體資源，則此操作或後續操作可能會拋出錯誤，如`MediaPlayerException`，然後退出。

當透過`MediaPlayer.prepareToPlay`準備播放時，事件的順序為：

1. `MediaPlayerEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 廣告。
1. `MediaPlayerEvent.STATUS_CHANGED` 狀態  `MediaPlayerStatus.PREPARED`

對於即時／線性串流，當播放視窗前進並解決其他機會時，事件順序為：

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 是否插入廣告

## 廣告活動順序{#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

當您的播放包含廣告時，TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件來實施動作。

播放廣告時，事件的順序為：

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

廣告分段內的每個廣告都會傳送下列事件：

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

下列範例顯示廣告播放事件的典型進展：

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## DRM事件順序{#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。 您的播放器可以實作回應這些事件的動作。

要獲得所有與DRM相關的事件的通知，請監聽`MediaPlayerEvent.DRM_METADATA`。 TVSDK會透過`DRMManager`類別分派其他DRM事件。

## 載入器事件的順序{#section_5638F8EDACCE422A9425187484D39DCC}

當載入器事件發生時，TVSDK會派單`MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`。