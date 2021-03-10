---
description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
title: Primetime播放器事件摘要
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# 黃金時段播放器事件摘要{#primetime-player-events-summary}

您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。

## 事件{#events}

TVSDK會在您的應用程式必須回應的事件發生時通知您。 每個事件都對應一個監聽器類，並帶有您必須實施的回調方法。

>[!TIP]
>
>事件代碼是`MediaPlayerEvent`枚舉的常數。

`AdBreakCompletedEventListener`

* **意** 思廣告插播的播放已完成。

* **要實作的回呼** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **意** 思在播放期間會略過廣告插播。

* **要實作的回呼** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **意** 思廣告插播已開始播放。

* **要實作的回呼** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

`AdClickedEventListener`

* **意** 思在播放期間點按了廣告。

* **要實作的回呼** `onAdClicked(AdClickEvent event)`
* **事件代碼** `AD_CLICK`

`AdCompletedEventListener`

* **意** 思廣告播放完成。

* **要實作的回呼** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

`AdProgressEventListener`

* **MaingReporting** 在播放期間進度。

* **要實作的回呼** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **MainingPrimetime廣** 告決策廣告解決方案已完成。此事件僅適用於VOD內容。

* **要實作的回呼** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意** 思廣告的播放已開始。

* **要實作的回呼** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

`AudioUpdatedEventListener`

* **意** 思已偵測到新的音軌。

* **要實作的回呼** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **意** 思播放器已開始緩衝。

* **要實作的回呼** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **意** 思播放器已停止緩衝。

* **要實作的回呼** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

`BufferPreparedEventListener&#39;&quot;

* **意** 思緩衝區已準備。

* **要實作的回呼** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **意** 義已偵測到新標題軌道。

* **要實作的回呼** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **意** 思在媒體串流中偵測到新的DRM中繼資料。

* **要實作的回呼** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

`ItemCreatedEventListener`

* **意** 思已建立新的媒體播放器項目。

* **要實作的回呼** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **意** 義已為當前項目建立新的載入資訊。

* **要實作的回呼** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

`LoadInformationEventListener`

* **意** 思已載入新區段。

* **要實作的回呼** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Meaning** 主要資訊清單或播放清單已更新。

* **要實作的回呼** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

`NotificationEventListener`

* **意** 思操作失敗。

* **要實作的回呼** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **意** 思播放範圍已更新。

* **要實作的回呼** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **意** 思螢幕上會顯示新的播放速率。

* **要實作的回呼** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **意** 思已設定MediaPlayer的rate屬性。

* **要實作的回呼** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

`PlayStartEventListener`

* **意** 思播放已開始。

* **要實作的回呼** `onPlayStart()`

* **事件代碼** `PLAY_START`

`ProfileChangeEventListener`

* **意** 思MediaPlayer的目前設定檔已變更。

* **要實作的回呼** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **MaingPlayback已** 達到時間軸保留。

* **要實作的回呼** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **MeaningSeek** 操作已啟動。

* **要實作的回呼** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

`SeekEndEventListener`

* **意** 思搜尋作業已完成。

* **要實作的回呼** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **意** 思搜尋位置已因內部播放規則或外部業務規則而調整。

* **要實作的回呼** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **意** 思介質大小可用。

* **要實作的回呼** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **意** 思MediaPlayer狀態已變更。

* **要實作的回呼** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

`TimeChangeEventListener`

* **意** 思播放頭已變更。

* **要實作的回呼** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

`TimedEventEventListener`

* **意** 思操作完成時間為操作所花費的時間。

* **要實作的回呼** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **意** 思新增計時中繼資料至背景中的項目。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **意** 思在媒體串流中偵測到新的計時中繼資料。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **意** 思時間軸已修改。廣告可能已新增至時間軸或從時間軸移除。

* **要實作的回呼** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`