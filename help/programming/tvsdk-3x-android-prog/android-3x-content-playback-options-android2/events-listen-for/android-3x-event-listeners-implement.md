---
description: 事件處理程式使您能夠響應TVSDK事件。
title: 實現事件偵聽器和回調
exl-id: 1f7977e3-4f96-4c0d-ae33-319c84a33ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 實現事件偵聽器和回調  {#implement-event-listeners-and-callbacks}

事件處理程式使您能夠響應TVSDK事件。

發生事件時，TVSDK的事件機制將調用註冊的事件處理程式，並將事件資訊傳遞給它。

TVSDK將監聽器定義為內部的公共內部介面 `MediaPlayer` 。

您的應用程式必須為影響您應用程式的任何TVSDK事件實施事件偵聽器。

1. 確定應用程式必須偵聽的事件。

   * 必需事件：收聽所有播放事件。

      >[!IMPORTANT]
      >
      >偵聽狀態更改事件，當玩家的狀態以您需要知道的方式發生更改時發生。 它提供的資訊包括可能影響播放器下一步操作的錯誤。

   * 有關其他事件，請參閱  [黃金時段玩家事件摘要](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)。

1. 為每個事件實現並添加事件偵聽器。

   對於大多數事件，TVSDK將參數傳遞給事件偵聽器。 這些值提供有關事件的資訊，可幫助您確定下一步的操作。 的 `MediaPlayerEvent` 枚舉列出所有 `MediaPlayer` 派單。 有關詳細資訊，請參見  [黃金時段玩家事件摘要](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)。

   例如，如果 `mPlayer` 是 `MediaPlayer`，下面是如何添加和構造事件偵聽器：

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

TVSDK按通常預期的序列調度事件/通知。 您的玩家可以根據預期序列中的事件執行操作。

以下示例顯示了在回放期間發生的某些事件的順序。

成功載入媒體資源時 `MediaPlayer.replaceCurrentResource`，事件順序為：

1. `MediaPlayerEvent.STATUS_CHANGED` 狀態 `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` 狀態 `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>在主線程上載入媒體資源。 如果在後台線程上載入媒體資源，則此操作或後續操作可能會引發錯誤，如 `MediaPlayerException`，然後退出。

準備通過 `MediaPlayer.prepareToPlay`，事件順序為：

1. `MediaPlayerEvent.STATUS_CHANGED` 狀態 `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` 插入廣告。
1. `MediaPlayerEvent.STATUS_CHANGED` 狀態 `MediaPlayerStatus.PREPARED`

對於即時/線性流，在回放期間，隨著回放窗口的提前和附加機會的解決，事件的順序是：

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` 如果插入廣告

## 廣告活動順序 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

當播放包括廣告時，TVSDK會按通常預期的序列發送事件/通知。 您的玩家可以根據預期序列中的事件執行操作。

在播放廣告時，事件的順序是：

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

廣告時段內的每個廣告都會調度以下事件：

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

以下示例顯示廣告播放事件的典型進展：

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

TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。 您的玩家可以實施響應這些事件的操作。

要獲知所有與DRM相關的事件，請收聽 `MediaPlayerEvent.DRM_METADATA`。 TVSDK通過 `DRMManager` 類。

## 載入程式事件順序 {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK派單 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 裝載程式事件發生時。
