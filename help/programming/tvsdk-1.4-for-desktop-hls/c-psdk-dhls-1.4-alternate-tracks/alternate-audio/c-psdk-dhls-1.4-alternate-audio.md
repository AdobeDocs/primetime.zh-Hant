---
description: 備用或延遲綁定的音頻允許您在視頻軌道的可用音頻軌道之間切換。 這樣，用戶可以在播放視頻時選擇語言軌道。
title: 備用音頻
exl-id: 0a40fbd9-f043-4296-9f07-d75bacf793f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 備用音頻{#alternate-audio}

備用或延遲綁定的音頻允許您在視頻軌道的可用音頻軌道之間切換。 這樣，用戶可以在播放視頻時選擇語言軌道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立 `MediaPlayerItem` 當前視頻的實例，將建立 `AudioTrack` 每個可用音頻軌道的項目。 該項包含 `name` 屬性，該字串通常包含該軌道語言的用戶可識別描述。 該項目還包含有關是否預設使用該跟蹤的資訊。

播放視頻時，您可以要求提供可用音頻軌道清單，或者讓用戶選擇一個，並設定視頻以與所選軌道一起播放。

雖然很少，但如果在建立 `MediaPlayerItem`,TVSDK將觸發 `MediaPlayerItem.AUDIO_UPDATED` 的子菜單。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支援備用音頻：

`hasAlternateAudio`

如果指定的介質具有備用音頻軌道（預設軌道除外），則此布爾函式將返回 `true`。 如果沒有備用音頻軌道，則函式返回 `false`。

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

此函式返回指定介質中所有當前可用音頻軌道的清單。

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

`getSelectedAudioTrack`

此函式返回當前選擇的備用音頻軌道和屬性（如語言）。 還可以提取軌跡的自動選擇。

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

此函式選擇要播放的備用音頻軌道。

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
