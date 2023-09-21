---
description: 您的應用程式可監聽TVSDK傳送的事件，以監控播放器中的活動和播放器狀態的變更。
title: Primetime播放器事件摘要
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Primetime播放器事件摘要 {#primetime-player-events-summary-overview}

您的應用程式可監聽TVSDK傳送的事件，以監控播放器中的活動和播放器狀態的變更。

## 活動 {#events}

TVSDK會在應用程式必須回應的事件發生時通知您。 每個事件都對應至監聽器類別，並附有您必須實作的回呼方法。

>[!TIP]
>
>事件程式碼是 `MediaPlayerEvent` 列舉。

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* **意義**廣告插播的播放完成。

* ** Callback以實作** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* **表示**播放期間略過廣告插播。

* ** Callback以實作** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* **意義**廣告插播的播放已開始。

* ** Callback以實作** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* **表示**播放期間有人點按廣告。

* ** Callback以實作** `onAdClicked(AdClickEvent event)`

* **事件代碼** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* **意義**廣告播放完成。

* ** Callback以實作** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* **表示**錄放期間報告進度。

* ** Callback以實作** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* **表示Primetime**Decisioningad解析已完成。 此事件僅適用於VOD內容。

* ** Callback以實作** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意義**廣告播放已開始。

* ** Callback以實作** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* **意義**偵測到新的音軌。

* ** Callback以實作** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* **意義**播放器已開始緩衝。

* ** Callback以實作** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* **表示**播放器已停止緩衝。

* ** Callback以實作** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* **意義**緩衝區已備妥。

* ** Callback以實作** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* **意義**偵測到新的註解追蹤。

* ** Callback以實作** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* **意義**已在媒體資料流中偵測到新的DRM中繼資料。

* ** Callback以實作** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* **含義**已建立新的媒體播放器專案。

* ** Callback以實作** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* **意義**已為目前專案建立新的載入資訊。

* ** Callback以實作** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* **表示**已載入新區段。

* ** Callback以實作** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* **意義**主要資訊清單或播放清單已更新。

* ** Callback以實作** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* **意義**作業已失敗。

* ** Callback以實作** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* **意義**播放範圍已更新。

* ** Callback以實作** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* **意義**新的播放速率會顯示在畫面上。

* ** Callback以實作** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* **表示**已設定MediaPlayer的rate屬性。

* ** Callback以實作** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* **意義**播放已開始。

* ** Callback以實作** `onPlayStart()`

* **事件代碼** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* **表示**MediaPlayer目前的設定檔已變更。

* ** Callback以實作** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

## ReservationReactedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* **表示播放**間已達到時間表保留區。

* ** Callback以實作** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* **表示**搜尋作業已開始。

* ** Callback以實作** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* **意義**搜尋作業已完成。

* ** Callback以實作** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* **意義**搜尋位置已因內部播放規則或外部商業規則而調整。

* ** Callback以實作** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* **意義**可用的媒體大小。

* ** Callback以實作** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* **表**MediaPlayer狀態已變更。

* ** Callback以實作** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* **表示**播放點已變更。

* ** Callback以實作** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* **意義**作業已完成，且作業已花費時間。

* ** Callback以實作** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* **意義**新的計時中繼資料已新增到背景中的專案。

* ** Callback以實作** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* **含義**在媒體資料流中偵測到新的計時中繼資料。

* ** Callback以實作** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* **表**時間軸已修改。 廣告可能已新增至時間軸，或從時間軸移除。

* ** Callback以實作** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`
