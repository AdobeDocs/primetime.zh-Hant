---
description: 您的應用程式可以通過偵聽TVSDK派送的事件來監視播放器中的活動和播放器的更改狀態。
title: 黃金時段玩家事件摘要
exl-id: 42489abe-ccaf-4b40-bb4b-de8547b5585a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# 黃金時段玩家事件摘要 {#primetime-player-events-summary-overview}

您的應用程式可以通過偵聽TVSDK派送的事件來監視播放器中的活動和播放器的更改狀態。

## 事件 {#events}

TVSDK會在您的應用程式必須響應的事件發生時通知您。 每個事件都與監聽器類相對應，並且必須實現回調方法。

>[!TIP]
>
>事件代碼是 `MediaPlayerEvent` 枚舉。

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* **意思**廣告中斷的播放已完成。

* **要實施的回調** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_COMPLETE`

## AdBreakSkpitedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* **意思**在播放期間跳過廣告中斷。

* **要實施的回調** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* **意思**廣告中斷的播放已開始。

* **要實施的回調** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代碼** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* **意思**在播放過程中按一下了廣告。

* **要實施的回調** `onAdClicked(AdClickEvent event)`

* **事件代碼** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* **意思**廣告的播放已完成。

* **要實施的回調** `onAdCompleted(AdPlaybackEvent event)`

* **事件代碼** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* **意思**播放期間報告進度。

* **要實施的回調** `onAdProgress(AdPlaybackEvent event)`

* **事件代碼** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* **意思**黃金時段廣告決策及解決已完成。 此事件僅適用於VOD內容。

* **要實施的回調** `onAdResolutionComplete()`

* **事件代碼** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* **意思**廣告的播放已開始。

* **要實施的回調** `onAdStarted(AdPlaybackEvent event)`

* **事件代碼** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* **意思**檢測到新的音頻軌道。

* **要實施的回調** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* **意思**玩家已開始緩衝。

* **要實施的回調** `onBufferingBegin(BufferEvent event)`

* **事件代碼** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* **意思**播放器已停止緩衝。

* **要實施的回調** `onBufferingEnd(BufferEvent event)`

* **事件代碼** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* **意思**緩衝區已準備好。

* **要實施的回調** `onBufferPrepared()`

* **事件代碼** `BUFFER_PREPARED`

## 標題UpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* **意思**檢測到新的字幕軌道。

* **要實施的回調** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* **意思**在媒體流中檢測到新的DRM元資料。

* **要實施的回調** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代碼** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* **意思**已建立新媒體播放器項目。

* **要實施的回調** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* **意思**已為當前項目建立新的載入資訊。

* **要實施的回調** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代碼** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* **意思**已載入新段。

* **要實施的回調** `onLoadInformation(LoadInformationEvent event)`

* **事件代碼** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* **意思**主清單或播放清單已更新。

* **要實施的回調** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* **表示**操作失敗。

* **要實施的回調** `onNotification(NotificationEvent event)`

* **事件代碼** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* **意思**播放範圍已更新。

* **要實施的回調** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代碼** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* **意思**螢幕上顯示新的播放速率。

* **要實施的回調** `onRatePlaying(PlaybackRateEvent event)`

* **事件代碼** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* **意思**已設定MediaPlayer的rate屬性。

* **要實施的回調** `onRateSelected(PlaybackRateEvent event)`

* **事件代碼** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* **意思**播放已開始。

* **要實施的回調** `onPlayStart()`

* **事件代碼** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* **意思** MediaPlayer的當前配置檔案已更改。

* **要實施的回調** `onProfileChanged(ProfileEvent event)`

* **事件代碼** `PROFILE_CHANGED`

## ReservationAchatedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* **意思**播放已達到時間線保留。

* **要實施的回調** `onReservationReached(ReservationEvent event)`

* **事件代碼** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* **意思**搜索操作已開始。

* **要實施的回調** `onSeekBegin(SeekEvent event)`

* **事件代碼** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* **意思**搜索操作已完成。

* **要實施的回調** `onSeekEnd(SeekEvent event)`

* **事件代碼** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* **意思**由於內部播放規則或外部業務規則而調整了查找位置。

* **要實施的回調** `onPositionAdjusted(SeekEvent event)`

* **事件代碼** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* **表示**介質大小可用。

* **要實施的回調** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代碼** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* **意思** MediaPlayer狀態已更改。

* **要實施的回調** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代碼** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* **意思**播放頭已更改。

* **要實施的回調** `onTimeChanged(TimeChangeEvent event)`

* **事件代碼** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* **意思**操作完成，且操作所花費的時間。

* **要實施的回調** `onTimedEvent(TimedEventEvent event)`

* **事件代碼** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* **意思**已將新的定時元資料添加到後台項目。

* **要實施的回調** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* **意思**在媒體流中檢測到新的定時元資料。

* **要實施的回調** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代碼** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* **意思**時間線已修改。 廣告可能已添加到時間軸或從時間軸中刪除。

* **要實施的回調** `onTimelineUpdated(TimelineEvent event)`

* **事件代碼** `TIMELINE_UPDATED`
