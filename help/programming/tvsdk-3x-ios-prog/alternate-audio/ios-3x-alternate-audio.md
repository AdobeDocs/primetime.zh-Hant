---
seo-title: 替代音訊
title: 替代音訊
uuid: cc38ded2-45b7-4be4-8f46-a919fdaf79cf
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 替代音訊 {#alternate-audio}

替代或延遲系結的音訊可讓您在視訊軌的可用音軌間切換。 如此，使用者就可在播放視訊時選取語言軌道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立目 `MediaPlayerItem` 前視訊的例項時，會為每個可用 `AudioTrack` 的音軌建立項目。 項目包含屬 `name` 性，此字串通常包含該追蹤語言的使用者可識別描述。 項目也包含是否依預設使用該追蹤的資訊。

在播放視訊時，您可以要求提供可用音軌的清單、選擇性讓使用者選擇一個音軌，並設定視訊與選取的音軌一起播放。

雖然很少，但若在建立音軌後有其他音軌可用， `MediaPlayerItem`TVSDK會觸發事 `MediaPlayerItem.AUDIO_UPDATED` 件。

## 新增API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已新增下列API以支援替代音訊：

**hasAlternateAudio**

如果指定的媒體有替代音軌（除預設音軌外），此布林值函式會傳回 `true`。 如果沒有替代音軌，函式會傳回 `false`。

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

**getAudioTracks**

此函式會傳回指定媒體中所有目前可用音軌的清單。

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
    if (_audioTracks) { 
        out = _audioTracks; 
        out->addRef(); 
        return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

**getSelectedAudioTrack**

此函式可傳回目前選取的替代音軌和屬性，例如語言。 還可以提取軌道的自動選擇。

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

**selectAudioTrack**

此函式會選取要播放的替代音軌。

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
