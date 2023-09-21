---
description: 事件處理常式可讓TVSDK回應事件。
title: 實作事件接聽程式和回呼
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# 實作事件接聽程式和回呼{#implement-event-listeners-and-callbacks}

事件處理常式可讓TVSDK回應事件。

當事件發生時，TVSDK的事件機制會呼叫您註冊的事件處理常式，並將事件資訊傳遞給處理常式。

TVSDK將監聽器定義為中的公用內部介面 `MediaPlayer` 介面。

您的應用程式必須為影響應用程式的TVSDK事件實作事件監聽器。

如需視訊分析的完整事件清單，請參閱追蹤核心視訊播放。

1. 決定應用程式必須監聽的事件。

   * **必要事件**：接聽所有播放事件。

     >[!IMPORTANT]
     >
     >播放事件 `onStateChanged` 提供播放器狀態，包括錯誤。 任何狀態都可能影響您的播放器的下一步

   * **其他事件**：選用，視您的應用程式而定。

     例如，如果您在播放中加入廣告，請實作AdPlaybackEventListener回呼。

1. 實作每個事件的事件接聽程式。

   TVSDK會傳回事件接聽程式回呼的引數值。 這些值會提供您可在接聽程式中用來執行適當動作的事件相關資訊。

   `MediaPlayer.EventListener` 列出所有回呼介面。 每個介面會顯示針對每個事件傳回的回呼名稱和引數。

   例如：

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. 向註冊回呼接聽程式 `MediaPlayer` 物件，使用 `MediaPlayer.addEventListener`.

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

TVSDK會以一般預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。

下列範例顯示包含播放事件之部分事件的順序。

* 當成功載入媒體資源透過 `MediaPlayer.replaceCurrentResource`，事件的順序為：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>將您的媒體資源載入主要執行緒。 如果您在背景執行緒載入媒體資源，此作業或後續TVSDK作業（或兩者）可能會擲回錯誤(例如， `IllegalStateException`)並退出。

* 準備透過播放 `MediaPlayer.prepareToPlay`，事件的順序為：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 是否已插入廣告。
1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayerStatus.PREPARED`

* 對於即時/線性串流，在播放視窗前進且其他機會解決時播放期間，事件的順序為：

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 如果已插入廣告
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` 如果已插入廣告

下列範例顯示事件的典型進度：

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

## 廣告活動的順序 {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

當您的播放包含廣告時，TVSDK會以通常預期的順序傳送事件/通知。 您的播放器可以根據預期序列中的事件實作動作。

播放廣告時，事件的順序為：

* `AdPlaybackEventListener.onAdBreakStart`
* 系統會為廣告插播中的每個廣告傳送以下內容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （廣告播放期間多次）
   * `AdPlaybackEventListener.onAdClick` （每次點按）
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

下列範例顯示廣告播放事件的典型延展：

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
* 系統會為廣告插播中的每個廣告傳送以下內容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （廣告播放期間多次）
   * `AdPlaybackEventListener.onAdClick` （每次點按）
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

下列範例顯示廣告播放事件的典型延展：

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

TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝和搜尋事件。

下列範例顯示這些事件的典型進度：

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

TVSDK會傳送數位版權管理(DRM)事件，以回應DRM相關作業，例如當新的DRM中繼資料可用時。 您的播放器可以實施動作來回應這些事件。

若要收到有關所有DRM相關事件的通知，請接聽 `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK會透過傳送其他DRM事件 `DRMManager` 類別。

下列範例顯示典型的進度：

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## 載入器事件 {#section_5638F8EDACCE422A9425187484D39DCC}

您的播放器可根據下列事件實作動作：

| 事件 | 含義 |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | 媒體資源載入已成功完成。 |
| `onError` | 媒體資源載入時發生問題。 |
