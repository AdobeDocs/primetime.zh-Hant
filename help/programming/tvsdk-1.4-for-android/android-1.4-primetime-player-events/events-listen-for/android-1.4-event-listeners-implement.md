---
description: 事件處理程式允許TVSDK響應事件。
title: 實現事件偵聽器和回調
exl-id: eda5cd4e-4ee8-4b37-a179-242e8697f61f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# 實現事件偵聽器和回調{#implement-event-listeners-and-callbacks}

事件處理程式允許TVSDK響應事件。

當發生事件時，TVSDK的事件機制將調用您註冊的事件處理程式並將事件資訊傳遞給處理程式。

TVSDK將監聽器定義為 `MediaPlayer` 。

您的應用程式必須為影響您的應用程式的TVSDK事件實現事件偵聽器。

有關視頻分析事件的完整清單，請參閱跟蹤核心視頻播放。

1. 確定應用程式必須偵聽哪些事件。

   * **必需事件**:收聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `onStateChanged` 提供播放器狀態，包括錯誤。 任何狀態都可能影響玩家的下一步

   * **其他事件**:可選，具體取決於您的應用程式。

      例如，如果在播放中合併廣告，則實施AdPlaybackEventListener回調。

1. 為每個事件實現事件偵聽器。

   TVSDK將參數值返回到事件監聽器回調。 這些值提供了有關事件的相關資訊，您可以在監聽器中使用這些事件執行相應的操作。

   `MediaPlayer.EventListener` 列出所有回調介面。 每個介面都顯示為每個事件返回的回調名稱和參數。

   例如：

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. 將回調偵聽器註冊到 `MediaPlayer` 對象使用 `MediaPlayer.addEventListener`。

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

TVSDK按通常預期的序列調度事件/通知。 您的玩家可以根據預期序列中的事件執行操作。

以下示例顯示了包含回放事件的某些事件的順序。

* 成功載入媒體資源時 `MediaPlayer.replaceCurrentResource`，事件順序為：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>在主線程上載入媒體資源。 如果在後台線程上載入媒體資源，則此操作或後續的TVSDK操作或兩者都可能引發錯誤(例如， `IllegalStateException`)並退出。

* 準備通過 `MediaPlayer.prepareToPlay`，事件順序為：

1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 插入廣告。
1. `MediaPlayer.PlaybackEventListener.onStateChanged` 狀態 `MediaPlayerStatus.PREPARED`

* 對於即時/線性流，在回放期間，隨著回放窗口的提前和附加機會的解決，事件的順序是：

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 如果插入廣告
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` 如果插入廣告

以下示例顯示了事件的典型進展：

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

當播放包括廣告時，TVSDK會按通常預期的序列發送事件/通知。 您的玩家可以根據預期序列中的事件執行操作。

在播放廣告時，事件的順序是：

* `AdPlaybackEventListener.onAdBreakStart`
* 廣告分段中的每個廣告都派發以下內容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （廣告播放期間多次）
   * `AdPlaybackEventListener.onAdClick` （對於每次按一下）
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

以下示例顯示廣告播放事件的典型進展：

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

在播放廣告時，事件的順序是：

* `AdPlaybackEventListener.onAdBreakStart`
* 廣告分段中的每個廣告都派發以下內容：

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` （廣告播放期間多次）
   * `AdPlaybackEventListener.onAdClick` （對於每次按一下）
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

以下示例顯示廣告播放事件的典型進展：

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

TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝和查找事件。

以下示例顯示了這些事件的典型進展：

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

TVSDK響應於諸如當新的DRM元資料變為可用時的DRM相關操作而調度數字權限管理(DRM)事件。 您的玩家可以實施響應這些事件的操作。

要獲知所有與DRM相關的事件，請收聽 `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`。 TVSDK通過 `DRMManager` 類。

以下示例顯示了典型的晉升：

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## 載入程式事件 {#section_5638F8EDACCE422A9425187484D39DCC}

您的播放器可以基於以下事件實施操作：

| 事件 | 意義 |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | 媒體資源載入已成功完成。 |
| `onError` | 載入媒體資源時出現問題。 |
