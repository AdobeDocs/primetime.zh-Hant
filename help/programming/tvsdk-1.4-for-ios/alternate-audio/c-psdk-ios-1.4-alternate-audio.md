---
description: 替代或延遲繫結的音訊可讓您在視訊曲目的可用音訊曲目之間切換。 如此一來，使用者就能在播放視訊時選取語言追蹤。
title: 替代音訊
exl-id: c8158888-2e2a-42a6-a948-dc6ba4ce7a9c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 概觀 {#alternate-audio-overview}

替代或延遲繫結的音訊可讓您在視訊曲目的可用音訊曲目之間切換。 如此一來，使用者就能在播放視訊時選取語言追蹤。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立 `MediaPlayerItem` 目前視訊的執行個體，會建立 `AudioTrack` 每個可用音軌的專案。 專案包含 `name` 屬性，字串，通常包含使用者可辨識的該曲目語言描述。 此專案也包含預設是否要使用該曲目的相關資訊。

輪到播放視訊時，您可以要求一份可用音訊曲目清單，選擇性地讓使用者選擇其中一個曲目，並設定要以選取的曲目播放視訊。

雖然很罕見，但如果其他音軌在建立 `MediaPlayerItem`，TVSDK會觸發 `MediaPlayerItem.AUDIO_UPDATED` 事件。

## 新增API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已新增下列API以支援替代音訊：

`hasAlternateAudio`

如果指定的媒體有預設音軌以外的替代音軌，此布林值函式會傳回 `true`. 如果沒有替代音軌，函式會傳回 `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

此函式傳回指定媒體中所有目前可用音訊曲目的清單。

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const 
    { 
        if (_audioTracks) 
        { 
            out = _audioTracks; 
            out->addRef(); 
            return kECSuccess; 
        } 
        return kECDataNotAvailable; 
    }
```

`getSelectedAudioTrack`

此函式傳回目前選取的替代音軌和屬性，例如語言。 也可以擷取自動選取軌跡。

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const 
{ 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

此函式選取要播放的替代音軌。

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) 
{ 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) 
    { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) 
        { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
