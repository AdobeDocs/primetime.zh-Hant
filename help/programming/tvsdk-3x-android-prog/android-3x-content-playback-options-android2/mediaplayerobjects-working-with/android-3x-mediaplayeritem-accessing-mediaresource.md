---
description: MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。
title: 用於存取MediaResource資訊的MediaPlayerItem方法
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# 用於存取MediaResource資訊的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem類別中的方法可讓您取得由載入的MediaResource所代表之內容資料流的相關資訊。

| 方法 | 說明 |
|--- |--- |
| **廣告標籤** |  |
| 清單`<String>` getAdTags() | 提供用於廣告投放流程的廣告標籤清單。 |
| **即時資料流** |  |
| 布林值isLive()； | 如果資料流為即時，則為True；如果為VOD，則為False。 |
| **受DRM保護** |  |
| 布林值isProtected()； | 如果資料流受到DRM保護，則為True。 |
| 清單`<DRMMetadataInfo>` getDRMMetadataInfos()； | 列出資訊清單中發現的所有DRM中繼資料物件。 |
| **隱藏式字幕** |  |
| 布林值hasClosedCaptions()； | 如果隱藏式字幕追蹤可供使用，則為True。 |
| 清單`<ClosedCaptionsTrack>` getClosedCationsTracks()； | 提供可用隱藏式字幕追蹤的清單。 |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack()； | 擷取目前使用SelectClosedCaptionsTrack選取的隱藏式字幕追蹤。 |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | 將隱藏式字幕軌跡設為目前的隱藏式字幕軌跡。 |
| **替代音軌** |  |
| 布林值hasAlternateAudio()； | 如果資料流有替代音訊曲目，則為True。 注意：主要（預設）音軌也是替代音軌清單的一部分。  Android適用的TVSDK會將主要音軌視為替代音軌清單中的專案之一。 因此，MediaPlayerItem.hasAlternateAudio傳回false的唯一情況是串流完全沒有音訊。 如果內容只有一個音軌，則此方法會傳回true，並且  `MediaPlayerItem.getAudioTracks`  傳回含有單一元素的清單（預設音軌）。 |
| 清單`<AudioTrack>` getAudioTracks()； | 提供可用替代音訊曲目的清單。 |
| AudioTrack getSelectedAudioTrack()； | 擷取使用selectAudioTrack選取的音軌。 |
| selectAudioTrack ( AudioTrack audioTrack ) | 選取音軌作為目前的音軌。 |
| **定時中繼資料** |  |
| 布林值hasTimedMetadata()； | 如果串流有關聯的計時中繼資料，則為True。 |
| 清單`<TimedMetadata>` getTimedMetadata()； | 提供與資料流相關聯的計時中繼資料物件清單。 |
| **多個設定檔（位元速率）** |
| 布林值isDynamic()； | 如果資料流是多位元速率(MBR)資料流，則為True。 |
| 清單`<Profile>` getProfiles()； | 提供相關位元速率設定檔的清單。 對於每個設定檔，您可以擷取其位元速率以及設定檔的高度和寬度。 |
| 設定檔getSelectedProfile() | 擷取目前選取的設定檔。 |
| **特技播放** |  |
| 布林值isTrickPlaySupported()； | 如果播放器支援快進、倒轉和恢復，則為True。 |
| 清單`< Float>` getAvailablePlaybackRates() | 提供特技播放功能內容中的可用播放率清單。 |
| 浮點數getSelectedPlaybackRate() | 擷取目前選取的播放速率。 |
| MediaPlayerItemConfig getConfig() | 傳回與此專案關聯的MediaPlayerItemConfig執行個體。 |
| **媒體資源** |  |
| MediaResource getResource()； | 傳回與此專案關聯的媒體資源。 |
| int getResourceId() | 傳回與此專案關聯的媒體識別碼。 此ID是在使用MediaPlayerItemLoader.load載入專案時設定。 |
