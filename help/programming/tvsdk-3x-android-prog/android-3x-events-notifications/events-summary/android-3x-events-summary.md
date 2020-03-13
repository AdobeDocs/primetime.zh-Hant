---
description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
seo-description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
seo-title: Primetime播放器事件摘要
title: Primetime播放器事件摘要
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Primetime播放器事件摘要 {#primetime-player-events-summary}

您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。

## 事件 {#events}

TVSDK會在您的應用程式必須回應的事件發生時通知您。 每個事件都對應一個監聽器類，並帶有您必須實施的回調方法。

>[!TIP]
>
>事件代碼是枚舉的常 `MediaPlayerEvent` 數。

`AdBreakCompletedEventListener`

* **意思** ：廣告插播的播放已完成。

* **要實作的回呼**`onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼**`AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **亦即** ，在播放期間會略過廣告插播。

* **要實作的回呼**`onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼**`AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **意思** ：廣告插播的播放已開始。

* **要實作的回呼**`onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼**`AD_BREAK_START`

`AdClickedEventListener`

* **亦即** ，在播放期間曾點按廣告。

* **要實作的回呼**`onAdClicked(AdClickEvent event)`
* **事件代碼**`AD_CLICK`

`AdCompletedEventListener`

* **意思** ：廣告的播放已完成。

* **要實作的回呼**`onAdCompleted(AdPlaybackEvent event)`

* **事件代碼**`AD_COMPLETE`

`AdProgressEventListener`

* **意指** 「播放期間報告進度」。

* **要實作的回呼**`onAdProgress(AdPlaybackEvent event)`

* **事件代碼**`AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **意思** : Primetime廣告決策廣告解決方案已完成。 此事件僅適用於VOD內容。

* **要實作的回呼**`onAdResolutionComplete()`

* **事件代碼**`AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意思** ：廣告的播放已開始。

* **要實作的回呼**`onAdStarted(AdPlaybackEvent event)`

* **事件代碼**`AD_START`

`AudioUpdatedEventListener`

* **意思** ：已偵測到新的音軌。

* **要實作的回呼**`onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼**`AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **意思** ：播放器已開始緩衝。

* **要實作的回呼**`onBufferingBegin(BufferEvent event)`

* **事件代碼**`BUFFERING_BEGIN`

`BufferingEndEventListener`

* **意思** ：播放器已停止緩衝。

* **要實作的回呼**`onBufferingEnd(BufferEvent event)`

* **事件代碼**`BUFFERING_END`

`BufferPreparedEventListener&#39;&quot;

* **意思** ：緩衝區已準備好。

* **要實作的回呼**`onBufferPrepared()`

* **事件代碼**`BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **意思** ：已偵測到新的標題軌道。

* **要實作的回呼**`onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼**`CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **意思** ：在媒體串流中已偵測到新的DRM中繼資料。

* **要實作的回呼**`onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼**`DRM_METADATA`

`ItemCreatedEventListener`

* **亦即** ，已建立新的媒體播放器項目。

* **要實作的回呼**`onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼**`ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **意思** ：已建立目前項目的新載入資訊。

* **要實作的回呼**`onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼**`ITEM_UPDATED`

`LoadInformationEventListener`

* **意思** ：已載入新區段。

* **要實作的回呼**`onLoadInformation(LoadInformationEvent event)`

* **事件代碼**`LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **意思** ：主要資訊清單或播放清單已更新。

* **要實作的回呼**`onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼**`MANIFEST_UPDATED`

`NotificationEventListener`

* **這表示** ，操作已失敗。

* **要實作的回呼**`onNotification(NotificationEvent event)`

* **事件代碼**`OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **意思** ：播放範圍已更新。

* **要實作的回呼**`onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼**`PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **這表示** ，新的播放速率會顯示在螢幕上。

* **要實作的回呼**`onRatePlaying(PlaybackRateEvent event)`

* **事件代碼**`RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **亦即** ，已設定MediaPlayer的rate屬性。

* **要實作的回呼**`onRateSelected(PlaybackRateEvent event)`

* **事件代碼**`RATE_SELECTED`

`PlayStartEventListener`

* **意思** ：播放已開始。

* **要實作的回呼**`onPlayStart()`

* **事件代碼**`PLAY_START`

`ProfileChangeEventListener`

* **這表示** MediaPlayer目前的設定檔已變更。

* **要實作的回呼**`onProfileChanged(ProfileEvent event)`

* **事件代碼**`PROFILE_CHANGED`

`ReservationReachedEventListener`

* **也就是說** ，播放已達到時間軸保留。

* **要實作的回呼**`onReservationReached(ReservationEvent event)`

* **事件代碼**`RESERVATION_REACHED`

`SeekBeginEventListener`

* **意思是** ，搜尋操作已開始。

* **要實作的回呼**`onSeekBegin(SeekEvent event)`

* **事件代碼**`SEEK_BEGIN`

`SeekEndEventListener`

* **意思** ：搜尋作業已完成。

* **要實作的回呼**`onSeekEnd(SeekEvent event)`

* **事件代碼**`SEEK_END`

`SeekPositionAdjustedEventListener`

* **意思** ：搜尋位置已因內部播放規則或外部業務規則而調整。

* **要實作的回呼**`onPositionAdjusted(SeekEvent event)`

* **事件代碼**`SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **意思** ：介質的大小是可用的。

* **要實作的回呼**`onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼**`SIZE_AVAILABLE`

`StatusChangeEventListener`

* **這表示** MediaPlayer狀態已變更。

* **要實作的回呼**`onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼**`STATUS_CHANGED`

`TimeChangeEventListener`

* **意思** ：播放磁頭已變更。

* **要實作的回呼**`onTimeChanged(TimeChangeEvent event)`

* **事件代碼**`TIME_CHANGED`

`TimedEventEventListener`

* **意思** ：此操作已完成，且所花費的時間為操作。

* **要實作的回呼**`onTimedEvent(TimedEventEvent event)`

* **事件代碼**`TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **意思** ：新的計時中繼資料已新增至背景中的項目。

* **要實作的回呼**`onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼**`TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **意思** ：在媒體串流中偵測到新的計時中繼資料。

* **要實作的回呼**`onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼**`TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **意思** ：時間軸已修改。 廣告可能已新增至時間軸或從時間軸移除。

* **要實作的回呼**`onTimelineUpdated(TimelineEvent event)`

* **事件代碼**`TIMELINE_UPDATED`