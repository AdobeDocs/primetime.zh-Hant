---
description: 您的應用程式可以監聽TVSDK所發送的事件，以監控播放器中的活動和播放器的變更狀態。
title: Primetime播放器事件摘要
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Primetime播放器事件摘要{#primetime-player-events-summary}

您的應用程式可以監聽TVSDK所發送的事件，以監控播放器中的活動和播放器的變更狀態。

## 事件 {#events}

TVSDK會在您的應用程式必須回應的事件發生時通知您。 每個事件都對應至監聽器類，並包含您必須實作的回呼方法。

>[!TIP]
>
>事件代碼是`MediaPlayerEvent`列舉的常數。

`AdBreakCompletedEventListener`

* **** 表示廣告插播的播放完成。

* **要實作的回呼** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** 這表示播放期間已略過廣告插播。

* **要實作的回呼** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** 表示廣告插播的播放已開始。

* **要實作的回呼** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

`AdClickedEventListener`

* **** 意指在播放期間曾點按廣告。

* **要實作的回呼** `onAdClicked(AdClickEvent event)`
* **事件代碼** `AD_CLICK`

`AdCompletedEventListener`

* **** 表示廣告播放完成。

* **要實作的回呼** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

`AdProgressEventListener`

* **** 播放期間進度的MaingReporting。

* **要實作的回呼** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** 意思Primetime廣告決策廣告解決已完成。此事件僅適用於VOD內容。

* **要實作的回呼** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** 表示廣告的播放已開始。

* **要實作的回呼** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

`AudioUpdatedEventListener`

* **** 意思偵測到新的音訊軌道。

* **要實作的回呼** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** 意思播放器已開始緩衝。

* **要實作的回呼** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** 意思播放器已停止緩衝。

* **要實作的回呼** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

`BufferPreparedEventListener`

* **** 含義緩衝區已準備。

* **要實作的回呼** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** 意思已偵測到新標題追蹤。

* **要實作的回呼** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** 意思在媒體資料流中偵測到新的DRM中繼資料。

* **要實作的回呼** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

`ItemCreatedEventListener`

* **** 表示已建立新的媒體播放器項目。

* **要實作的回呼** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** 表示已為當前項建立新載入資訊。

* **要實作的回呼** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** 表示已載入新區段。

* **要實作的回呼** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** 意思主要資訊清單或播放清單已更新。

* **要實作的回呼** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** 意思操作失敗。

* **要實作的回呼** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** 表示播放範圍已更新。

* **要實作的回呼** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** 這表示畫面上會顯示新的播放率。

* **要實作的回呼** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** 這表示已設定MediaPlayer的速率屬性。

* **要實作的回呼** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

`PlayStartEventListener`

* **** 表示播放已開始。

* **要實作的回呼** `onPlayStart()`

* **事件代碼** `PLAY_START`

`ProfileChangeEventListener`

* **** 這表示MediaPlayer的目前設定檔已變更。

* **要實作的回呼** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** MaingPlayback達到時間軸預訂。

* **要實作的回呼** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **** MaingSeek操作已開始。

* **要實作的回呼** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

`SeekEndEventListener`

* **** 意義搜尋操作已完成。

* **要實作的回呼** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** 意思搜尋位置已因內部播放規則或外部業務規則而調整。

* **要實作的回呼** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** 表示可用的媒體大小。

* **要實作的回呼** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** 這表示MediaPlayer狀態已變更。

* **要實作的回呼** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** 意思播放點已變更。

* **要實作的回呼** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

`TimedEventEventListener`

* **** 意義操作已完成，操作所花費的時間。

* **要實作的回呼** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** 意思背景中的項目已新增計時中繼資料。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** 意思媒體資料流中偵測到新的計時中繼資料。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** 意思時間軸已修改。廣告可能已新增至時間軸或從時間軸移除。

* **要實作的回呼** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`
