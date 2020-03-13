---
description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
seo-description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
seo-title: Primetime播放器事件摘要
title: Primetime播放器事件摘要
uuid: ed3be4c2-8df3-4d96-a30b-74c196262798
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# Primetime播放器事件摘要 {#primetime-player-events-summary-overview}

您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。

## 事件 {#events}

TVSDK會在您的應用程式必須回應的事件發生時通知您。 每個事件都對應一個監聽器類，並帶有您必須實施的回調方法。

>[!TIP]
>
>事件代碼是枚舉的常 `MediaPlayerEvent` 數。

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* **意思**廣告插播已完成。

* **要實作的回呼** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

## AdBreakKliptedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* **意指**在播放期間跳過廣告插播。

* **要實作的回呼** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* **意思**廣告插播已開始播放。

* **要實作的回呼** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* **意指**在播放期間點選了廣告。

* **要實作的回呼** `onAdClicked(AdClickEvent event)`

* **事件代碼** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* **意思**廣告播放完成。

* **要實作的回呼** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* **意指**播放期間報告進度。

* **要實作的回呼** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* **意思** Primetime廣告決策及解決方案已完成。 此事件僅適用於VOD內容。

* **要實作的回呼** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意思**廣告播放已開始。

* **要實作的回呼** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* **意思**已偵測到新的音軌。

* **要實作的回呼** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* **意思**播放器已開始緩衝。

* **要實作的回呼** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* **意思**播放器已停止緩衝。

* **要實作的回呼** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* **意思**已準備緩衝區。

* **要實作的回呼** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* **意思**已偵測到新的標題軌道。

* **要實作的回呼** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* **意思**在媒體串流中偵測到新的DRM中繼資料。

* **要實作的回呼** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* **意指**已建立新的媒體播放器項目。

* **要實作的回呼** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* **意思**已建立目前項目的新載入資訊。

* **要實作的回呼** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* **意思**已載入新區段。

* **要實作的回呼** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* **意思**主要資訊清單或播放清單已更新。

* **要實作的回呼** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* **意思**操作失敗。

* **要實作的回呼** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* **意指**播放範圍已更新。

* **要實作的回呼** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* **意思**螢幕上會顯示新的播放速率。

* **要實作的回呼** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* **意指**已設定MediaPlayer的rate屬性。

* **要實作的回呼** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* **意思**播放已開始。

* **要實作的回呼** `onPlayStart()`

* **事件代碼** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* **意指** MediaPlayer的目前設定檔已變更。

* **要實作的回呼** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* **意思是**播放達到時間軸預訂。

* **要實作的回呼** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* **意思**開始搜尋操作。

* **要實作的回呼** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* **意思**搜索操作已完成。

* **要實作的回呼** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* **意思**由於內部播放規則或外部業務規則，搜尋位置已調整。

* **要實作的回呼** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* **意思**介質大小可用。

* **要實作的回呼** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* **意思** MediaPlayer狀態已變更。

* **要實作的回呼** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* **意思**播放頭已變更。

* **要實作的回呼** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* **意思**操作完成，所需時間為操作。

* **要實作的回呼** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* **意思**新的計時中繼資料已新增至背景項目。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* **意指**在媒體串流中偵測到新的計時中繼資料。

* **要實作的回呼** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* **意思**時間軸已修改。 廣告可能已新增至時間軸或從時間軸移除。

* **要實作的回呼** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`