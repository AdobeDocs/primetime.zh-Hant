---
description: MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。
title: 用於訪問MediaResource資訊的MediaPlayerItem方法
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# 用於訪問MediaResource資訊的MediaPlayerItem方法 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem類中的方法允許您獲取有關由載入的MediaResource表示的內容流的資訊。

| 方法 | 說明 |
|--- |--- |
| **廣告標籤** |  |
| 清單`<String>` getAdTags() | 提供用於廣告放置過程的廣告標籤清單。 |
| **即時流** |  |
| boolean isLive(); | 如果流是活的，則為true;如果為VOD，則為false。 |
| **受DRM保護** |  |
| boolean isProtected(); | 如果流受DRM保護，則為True。 |
| 清單`<DRMMetadataInfo>` getDRMMetadataInfos(); | 列出清單中發現的所有DRM元資料對象。 |
| **隱藏字幕** |  |
| 布爾型hasClosedCaptions(); | 如果隱藏字幕磁軌可用，則為True。 |
| 清單`<ClosedCaptionsTrack>` getClosedActionsTracks(); | 提供可用的隱藏字幕軌道清單。 |
| ClosedCaptionsTrack獲取SelectedClosedCaptionsTrack(); | 檢索使用SelectClosedCaptionsTrack選擇的當前隱藏字幕軌道。 |
| selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) | 將隱藏字幕軌道設定為當前隱藏字幕軌道。 |
| **備用音頻軌道** |  |
| 布爾型hasAlternateAudio(); | 如果流具有備用音頻軌道，則為True。 注：主音軌（預設）也是備用音軌清單的一部分。  用於Android的TVSDK認為主音頻軌道是備用音頻軌道清單中的項目之一。 因此， MediaPlayerItem.hasAlternateAudio返回false的唯一情況是流根本沒有音頻。 如果內容只有一個音頻軌道，則此方法返回true,  `MediaPlayerItem.getAudioTracks`  返回包含單個元素（預設音頻軌道）的清單。 |
| 清單`<AudioTrack>` getAudioTracks(); | 提供可用備用音頻軌道的清單。 |
| AudioTrack getSelectedAudioTrack(); | 檢索使用selectAudioTrack選擇的音頻軌道。 |
| 選擇AudioTrack(AudioTrack audioTrack) | 選擇要成為當前音頻軌道的音頻軌道。 |
| **定時元資料** |  |
| 布爾型hasTimedMetadata(); | 如果流已關聯定時元資料，則為True。 |
| 清單`<TimedMetadata>` getTimedMetadata(); | 提供與流關聯的定時元資料對象的清單。 |
| **多個配置檔案（位速率）** |
| boolean isDynamic(); | 如果流是多比特率(MBR)流，則為True。 |
| 清單`<Profile>` getProfiles(); | 提供關聯比特率配置檔案的清單。 對於每個輪廓，可檢索其位速率以及輪廓的高度和寬度。 |
| 配置檔案getSelectedProfile() | 檢索當前選定的配置檔案。 |
| **戲法** |  |
| boolean isTrickPlaySupported(); | 如果玩家支援快速前進、倒帶和恢復，則為true。 |
| 清單`< Float>` getAvailablePlaybackRates() | 提供特技播放功能上下文中可用播放速率的清單。 |
| 浮點getSelectedPlaybackRate() | 檢索當前選定的播放速率。 |
| MediaPlayerItemConfig getConfig() | 返回與此項關聯的MediaPlayerItemConfig實例。 |
| **媒體資源** |  |
| MediaResource getResource(); | 返回與此項關聯的媒體資源。 |
| int getResourceId() | 返回與此項關聯的媒體標識符。 使用MediaPlayerItemLoader.load載入項時，將設定此ID。 |
