---
description: 事件處理常式可讓TVSDK回應事件。
seo-description: 事件處理常式可讓TVSDK回應事件。
seo-title: 實作事件偵聽器和回呼
title: 實作事件偵聽器和回呼
uuid: 6b7859a4-55f9-48b1-b1f1-7b79bc92610a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 實作事件偵聽器和回呼{#implement-event-listeners-and-callbacks}

事件處理常式可讓TVSDK回應事件。

發生事件時，TVSDK的事件機制會呼叫您已註冊的事件處理常式，並將事件資訊傳遞給處理常式。

TVSDK將監聽器定義為介面中的公用內部 `MediaPlayer` 介面。

您的應用程式必須針對影響您應用程式的TVSDK事件實作事件接聽程式。

如需視訊分析事件的完整清單，請參閱追蹤核心視訊播放。

1. 決定您的應用程式必須監聽哪些事件。

   * **必要事件**:監聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `onStateChanged` 提供播放器狀態，包括錯誤。 任何狀態都可能會影響您播放器的下一步

   * **其他事件**:可選，視您的應用程式而定。

      例如，如果您在播放中整合廣告，請實作AdPlaybackEventListener回呼。

1. 為每個事件實施事件偵聽器。

   TVSDK會將參數值傳回至您的事件接聽程式回呼。 這些值會提供有關事件的相關資訊，您可在監聽程式中用來執行適當動作。

   `MediaPlayer.EventListener` 列出所有回呼介面。 每個介面會顯示每個事件傳回的回呼名稱和參數。

   例如：

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. 使用將回呼偵聽程式註冊 `MediaPlayer` 到對象中 `MediaPlayer.addEventListener`。

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## 播放事件的順序 {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK會依照一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

下列範例顯示包含播放事件的某些事件的順序。

* 成功載入媒體資源時， `MediaPlayer.replaceCurrentResource`事件順序為：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>在主線程上載入媒體資源。 如果您在背景執行緒上載入媒體資源，此作業或後續的TVSDK作業（或兩者）可能會擲回錯誤(例如 `IllegalStateException`)並退出。

* 在準備播放時， `MediaPlayer.prepareToPlay`事件的順序為：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 廣告。
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayerStatus.PREPARED`

* 對於即時／線性串流，當播放視窗前進並解決其他機會時，事件順序為：

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 是否插入廣告
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` 是否插入廣告

下列範例顯示事件的典型進展：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## 廣告活動順序 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

當您的播放包含廣告時，TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

播放廣告時，事件的順序為：

* `AdPlaybackEventListener.onAdBreakStart`
* 廣告插播中的每個廣告都會傳送下列訊息：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （在廣告播放期間多次）
   * `AdPlaybackEventListener.onAdClick` （每次點按時）
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

下列範例顯示廣告播放事件的典型進展：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

播放廣告時，事件的順序為：

* `AdPlaybackEventListener.onAdBreakStart`
* 廣告插播中的每個廣告都會傳送下列訊息：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （在廣告播放期間多次）
   * `AdPlaybackEventListener.onAdClick` （每次點按時）
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

下列範例顯示廣告播放事件的典型進展：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## QoS事件 {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算，例如緩衝和搜尋事件。

下列範例顯示這些事件的典型進展：

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## DRM事件 {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK響應於DRM相關操作（例如當有新的DRM元資料可用時）來調度數字版權管理(DRM)事件。 您的播放器可以實作回應這些事件的動作。

要獲得所有與DRM相關的事件的通知，請監聽 `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`。 TVSDK會透過類別發佈其他DRM `DRMManager` 事件。

以下示例顯示典型的進度：

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## 載入器事件 {#section_5638F8EDACCE422A9425187484D39DCC}

您的播放器可以根據下列事件實作動作：

| 事件 | 意義 |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | 媒體資源載入成功完成。 |
| `onError` | 載入介質資源時發生問題。 |

