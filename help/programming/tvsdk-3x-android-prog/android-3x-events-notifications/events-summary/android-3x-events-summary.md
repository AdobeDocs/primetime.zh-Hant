---
description: 您的應用程式可以通過偵聽TVSDK派送的事件來監視播放器中的活動和播放器的更改狀態。
title: 黃金時段玩家事件摘要
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 黃金時段玩家事件摘要 {#primetime-player-events-summary}

您的應用程式可以通過偵聽TVSDK派送的事件來監視播放器中的活動和播放器的更改狀態。

## 事件 {#events}

TVSDK會在您的應用程式必須響應的事件發生時通知您。 每個事件都與監聽器類相對應，並且必須實現回調方法。

>[!TIP]
>
>事件代碼是 `MediaPlayerEvent` 枚舉。

`AdBreakCompletedEventListener`

* **意義** 廣告中斷的播放已完成。

* **要實現的回調** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **意義** 播放期間跳過了廣告中斷。

* **要實現的回調** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **意義** 已開始播放廣告中斷。

* **要實現的回調** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

`AdClickedEventListener`

* **意義** 播放期間按一下了廣告。

* **要實現的回調** `onAdClicked(AdClickEvent event)`
* **事件代碼** `AD_CLICK`

`AdCompletedEventListener`

* **意義** 廣告播放完畢。

* **要實現的回調** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

`AdProgressEventListener`

* **意義** 播放期間報告進度。

* **要實現的回調** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **意義** 黃金時段廣告決策結束。 此事件僅適用於VOD內容。

* **要實現的回調** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意義** 已開始播放廣告。

* **要實現的回調** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

`AudioUpdatedEventListener`

* **意義** 檢測到新的音頻軌道。

* **要實現的回調** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **意義** 玩家已開始緩衝。

* **要實現的回調** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **意義** 玩家已停止緩衝。

* **要實現的回調** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

`BufferPreparedEventListener`

* **意義** 準備緩衝器。

* **要實現的回調** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **意義** 檢測到新的字幕軌道。

* **要實現的回調** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **意義** 在媒體流中檢測到新的DRM元資料。

* **要實現的回調** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

`ItemCreatedEventListener`

* **意義** 已建立新媒體播放器項。

* **要實現的回調** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **意義** 已為當前項目建立新的載入資訊。

* **要實現的回調** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

`LoadInformationEventListener`

* **意義** 已載入新段。

* **要實現的回調** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **意義** 主清單或播放清單已更新。

* **要實現的回調** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

`NotificationEventListener`

* **意義** 操作失敗。

* **要實現的回調** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **意義** 播放範圍已更新。

* **要實現的回調** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **意義** 螢幕上可看到新的播放速率。

* **要實現的回調** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **意義** 已設定MediaPlayer的速率屬性。

* **要實現的回調** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

`PlayStartEventListener`

* **意義** 播放已開始。

* **要實現的回調** `onPlayStart()`

* **事件代碼** `PLAY_START`

`ProfileChangeEventListener`

* **意義** MediaPlayer的當前配置檔案已更改。

* **要實現的回調** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **意義** 播放已達到時間線保留。

* **要實現的回調** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **意義** 搜索操作已啟動。

* **要實現的回調** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

`SeekEndEventListener`

* **意義** 查找操作已完成。

* **要實現的回調** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **意義** 由於內部播放規則或外部業務規則，已調整查找位置。

* **要實現的回調** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **意義** 介質大小可用。

* **要實現的回調** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **意義** MediaPlayer狀態已更改。

* **要實現的回調** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

`TimeChangeEventListener`

* **意義** 玩家頭變了。

* **要實現的回調** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

`TimedEventEventListener`

* **意義** 該操作已完成，且所花費的時間已完成。

* **要實現的回調** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **意義** 已將新的定時元資料添加到後台項。

* **要實現的回調** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **意義** 在媒體流中檢測到新的定時元資料。

* **要實現的回調** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **意義** 時間線已修改。 廣告可能已添加到時間軸或從時間軸中刪除。

* **要實現的回調** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`
