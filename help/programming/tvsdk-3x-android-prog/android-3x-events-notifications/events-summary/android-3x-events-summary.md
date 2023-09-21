---
description: 您的應用程式可監聽TVSDK傳送的事件，以監控播放器中的活動和播放器狀態的變更。
title: Primetime播放器事件摘要
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Primetime播放器事件摘要 {#primetime-player-events-summary}

您的應用程式可監聽TVSDK傳送的事件，以監控播放器中的活動和播放器狀態的變更。

## 活動 {#events}

TVSDK會在應用程式必須回應的事件發生時通知您。 每個事件都對應至監聽器類別，並附有您必須實作的回呼方法。

>[!TIP]
>
>事件程式碼是 `MediaPlayerEvent` 列舉。

`AdBreakCompletedEventListener`

* **含義** 廣告插播的播放完成。

* **要實作的回呼** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **含義** 錄放期間已略過廣告插播。

* **要實作的回呼** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **含義** 廣告插播的播放已開始。

* **要實作的回呼** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

`AdClickedEventListener`

* **含義** 廣告在播放期間被點按。

* **要實作的回呼** `onAdClicked(AdClickEvent event)`
* **事件代碼** `AD_CLICK`

`AdCompletedEventListener`

* **含義** 廣告播放完成。

* **要實作的回呼** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

`AdProgressEventListener`

* **含義** 在播放期間報告進度。

* **要實作的回呼** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **含義** Primetime ad decisioningad解析已完成。 此事件僅適用於VOD內容。

* **要實作的回呼** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **含義** 廣告播放已開始。

* **要實作的回呼** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

`AudioUpdatedEventListener`

* **含義** 偵測到新的音軌。

* **要實作的回呼** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **含義** 播放器已開始緩衝。

* **要實作的回呼** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **含義** 播放器已停止緩衝。

* **要實作的回呼** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

`BufferPreparedEventListener`

* **含義** 已準備緩衝區。

* **要實作的回呼** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **含義** 偵測到新的標題追蹤。

* **要實作的回呼** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **含義** 已在媒體資料流中偵測到新的DRM中繼資料。

* **要實作的回呼** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

`ItemCreatedEventListener`

* **含義** 已建立新的媒體播放器專案。

* **要實作的回呼** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **含義** 已為目前專案建立新的載入資訊。

* **要實作的回呼** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

`LoadInformationEventListener`

* **含義** 已載入新區段。

* **要實作的回呼** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **含義** 已更新主要資訊清單或播放清單。

* **要實作的回呼** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

`NotificationEventListener`

* **含義** 操作失敗。

* **要實作的回呼** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **含義** 已更新播放範圍。

* **要實作的回呼** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **含義** 畫面上會顯示新的播放速率。

* **要實作的回呼** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **含義** 已設定MediaPlayer的rate屬性。

* **要實作的回呼** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

`PlayStartEventListener`

* **含義** 已開始播放。

* **要實作的回呼** `onPlayStart()`

* **事件代碼** `PLAY_START`

`ProfileChangeEventListener`

* **含義** MediaPlayer目前的設定檔已變更。

* **要實作的回呼** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **含義** 播放達到時間軸保留區。

* **要實作的回呼** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **含義** 搜尋作業已開始。

* **要實作的回呼** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

`SeekEndEventListener`

* **含義** 搜尋作業已完成。

* **要實作的回呼** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **含義** 搜尋位置已因內部播放規則或外部商業規則而調整。

* **要實作的回呼** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **含義** 媒體大小可供使用。

* **要實作的回呼** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **含義** MediaPlayer狀態已變更。

* **要實作的回呼** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

`TimeChangeEventListener`

* **含義** 播放點已變更。

* **要實作的回呼** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

`TimedEventEventListener`

* **含義** 作業已完成，且作業已花費時間。

* **要實作的回呼** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **含義** 已將新的計時中繼資料新增到背景中的專案。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **含義** 在媒體串流中偵測到新的計時中繼資料。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **含義** 已修改時間軸。 廣告可能已新增至時間軸，或從時間軸移除。

* **要實作的回呼** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`
