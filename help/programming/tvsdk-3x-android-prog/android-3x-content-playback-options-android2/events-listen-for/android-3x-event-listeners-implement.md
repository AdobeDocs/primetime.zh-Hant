---
description: 事件處理常式可讓您回應TVSDK事件。
title: 實作事件接聽程式和回呼
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 實作事件接聽程式和回呼  {#implement-event-listeners-and-callbacks}

事件處理常式可讓您回應TVSDK事件。

當事件發生時，TVSDK的事件機制會呼叫您註冊的事件處理常式，向其傳遞事件資訊。

TVSDK將監聽器定義為內的公用內部介面 `MediaPlayer` 介面。

您的應用程式必須針對任何影響您應用程式的TVSDK事件實作事件接聽程式。

1. 決定應用程式必須監聽的事件。

   * 必要事件：接聽所有播放事件。

     >[!IMPORTANT]
     >
     >聆聽狀態變更事件，當播放器的狀態以您需要瞭解的方式變更時，就會發生此事件。 它提供的資訊包含可能會影響您的播放器後續操作的錯誤。

   * 如需其他事件，請根據您的應用程式參閱  [Primetime播放器事件摘要](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. 實作並新增每個事件的事件監聽器。

   對於大多數事件，TVSDK會將引數傳給事件接聽程式。 這類值會提供關於事件的資訊，可協助您決定後續要執行的動作。 此 `MediaPlayerEvent` 列舉列出所有符合下列條件的事件： `MediaPlayer` dispatches. 如需詳細資訊，請參閱  [Primetime播放器事件摘要](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   例如，如果 `mPlayer` 為的例項 `MediaPlayer`，以下為新增及建構事件接聽程式的方法：

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

## 播放事件的順序 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK會以一般預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。

下列範例顯示播放期間發生的一些事件的順序。

當成功載入媒體資源透過 `MediaPlayer.replaceCurrentResource`，事件的順序為：

1. `MediaPlayerEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>將您的媒體資源載入主要執行緒。 如果您在背景執行緒載入媒體資源，此作業或後續作業可能會擲回錯誤，例如 `MediaPlayerException`，並退出。

準備透過播放 `MediaPlayer.prepareToPlay`，事件的順序為：

1. `MediaPlayerEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 是否已插入廣告。
1. `MediaPlayerEvent.STATUS_CHANGED` 具有狀態 `MediaPlayerStatus.PREPARED`

對於即時/線性串流，在播放視窗前進且其他機會解決時播放期間，事件的順序為：

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 如果已插入廣告

## 廣告活動的順序 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

當您的播放包含廣告時，TVSDK會以通常預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。

播放廣告時，事件的順序為：

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

系統會為廣告插播中的每個廣告傳送以下事件：

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

下列範例顯示廣告播放事件的典型延展：

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

## DRM事件順序 {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關作業，例如當新的DRM中繼資料可用時。 您的播放器可以實施動作來回應這些事件。

若要收到有關所有DRM相關事件的通知，請接聽 `MediaPlayerEvent.DRM_METADATA`. TVSDK會透過傳送其他DRM事件 `DRMManager` 類別。

## 載入器事件的順序 {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK傳送作業 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 載入器事件發生時。
