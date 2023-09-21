---
description: 替代音訊可讓您切換視訊曲目的可用音軌。 使用者可以選擇播放視訊時偏好的語言追蹤。
title: 替代音訊
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 概觀 {#alternate-audio-overview}

替代音訊可讓您切換視訊曲目的可用音軌。 使用者可以選擇播放視訊時偏好的語言追蹤。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立 `MediaPlayerItem` 例項中，會建立 `AudioTrack` 每個可用音軌的專案。 專案包含 `name` 屬性，這個字串通常包含使用者可辨識的該曲目語言描述。 此專案也包含預設是否要使用該追蹤的相關資訊。 當播放視訊時，您可以要求可用的音訊曲目清單，選擇性地允許使用者選取曲目，並設定視訊播放選取的曲目。

>[!TIP]
>
>雖然很罕見，但在TVSDK建立 `MediaPlayerItem`，TVSDK會觸發 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 事件。

## 新增API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已新增下列API以支援替代音訊：

`hasAlternateAudio`

如果指定的媒體有預設音軌以外的替代音軌，此布林值函式會傳回 `true`. 如果沒有替代音軌，函式會傳回 `false`.

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

此函式傳回指定媒體中所有目前可用的音訊曲目的清單。

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

此函式傳回目前選取的替代音軌和屬性，例如語言。 也可以擷取自動選取軌跡。

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

此函式選取要播放的替代音軌。

```java
void selectAudioTrack(AudioTrack audioTrack);
```

例如：

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```
