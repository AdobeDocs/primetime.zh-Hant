---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: MediaPlayerItem存取MediaResource資訊的方法
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# 用於訪問MediaResource資訊{#mediaplayeritem-methods-for-accessing-mediaresource-information}的MediaPlayerItem方法

MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。

| 方法 | 說明 |
|--- |--- |
| **廣告標籤** |  |
| List`<String>` getAdTags() | 提供用於廣告放置程式的廣告標籤清單。 |
| **即時串流** |  |
| boolean isLive(); | 如果串流是即時的，則為true;false（如果是VOD）。 |
| **受DRM保護** |  |
| boolean isProtected(); | 如果流受DRM保護，則為true。 |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | 列出在資訊清單中發現的所有DRM中繼資料物件。 |
| **隱藏字幕** |  |
| boolean hasClosedCaptions(); | 如果隱藏字幕音軌可用，則為true。 |
| List`<ClosedCaptionsTrack>` getClosedConsedActionsTracks(); | 提供可用隱藏字幕音軌的清單。 |
| ClosedCaptionsTrack獲取SelectedClosedCaptionsTrack(); | 擷取使用SelectClosedCaptionsTrack選取的目前隱藏字幕軌道。 |
| selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) | 將隱藏字幕軌道設定為當前隱藏字幕軌道。 |
| **替代音軌** |  |
| boolean hasAlternateAudio(); | 如果串流有替代的音軌，則為true。 注意： 主音軌（預設）也是替代音軌清單的一部分。  適用於Android的TVSDK會將主要音軌視為替代音軌清單中的項目之一。 因此，MediaPlayerItem.hasAlternateAudio傳回false的唯一情況是當串流完全沒有音訊時。 如果內容只有一個音軌，此方法會傳回true，而`MediaPlayerItem.getAudioTracks`會傳回包含單一元素（預設音軌）的清單。 |
| List`<AudioTrack>` getAudioTracks(); | 提供可用替代音軌的清單。 |
| AudioTrack getSelectedAudioTrack(); | 擷取使用selectAudioTrack選取的音軌。 |
| selectAudioTrack（AudioTrack音訊Track） | 選擇音軌作為當前音軌。 |
| **計時中繼資料** |  |
| boolean hasTimedMetadata(); | 如果串流已關聯計時中繼資料，則返回true。 |
| List`<TimedMetadata>` getTimedMetadata(); | 提供與流相關聯的定時元資料對象的清單。 |
| **多個描述檔（位元速率）** |
| boolean isDynamic(); | 如果流是多位速率(MBR)流，則為true。 |
| List`<Profile>` getProfiles(); | 提供關聯位速率配置檔案的清單。 對於每個配置檔案，可以檢索其位速率以及配置檔案的高度和寬度。 |
| 設定檔getSelectedProfile() | 擷取目前選取的描述檔。 |
| **特技遊戲** |  |
| boolean isTrickPlaySupported(); | 如果播放器支援快速前進、倒轉和繼續，則為true。 |
| List`< Float>` getAvailablePlaybackRates() | 提供特技播放功能內容中可用播放速率的清單。 |
| 浮動getSelectedPlaybackRate() | 擷取目前選取的播放速率。 |
| MediaPlayerItemConfig getConfig() | 傳回與此項目相關聯的MediaPlayerItemConfig例項。 |
| **媒體資源** |  |
| MediaResource getResource(); | 傳回與此項目關聯的媒體資源。 |
| int getResourceId() | 傳回與此項目相關的媒體識別碼。 此ID是在使用MediaPlayerItemLoader.load載入項目時設定。 |