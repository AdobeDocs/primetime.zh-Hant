---
description: 替代音效可讓您在視訊音軌的可用音軌間切換。 當視訊播放時，使用者可以選擇偏好的語言軌道。
title: 替代音訊
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 概述{#alternate-audio-overview}

替代音效可讓您在視訊音軌的可用音軌間切換。 當視訊播放時，使用者可以選擇偏好的語言軌道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立目前視訊的`MediaPlayerItem`例項時，會為每個可用的音軌建立`AudioTrack`項目。 項目包含`name`屬性，此屬性是字串，通常包含該追蹤語言的使用者可識別描述。 項目也包含是否依預設使用該追蹤的資訊。 在播放視訊時，您可以要求提供可用音軌清單、選擇性允許使用者選擇音軌，並設定視訊與選取的音軌一起播放。

>[!TIP]
>
>雖然很少，但若TVSDK在建立`MediaPlayerItem`後有其他音軌可供使用，TVSDK會觸發`MediaPlayerItem.AUDIO_TRACK_UPDATED`事件。

## 新增API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已新增下列API以支援替代音訊：

**`hasAlternateAudio`**

如果指定的媒體具有預設音軌以外的替代音軌，則此布爾函式返回`true`。 如果沒有替代音軌，函式將返回`false`。

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

此函式會傳回指定媒體中所有目前可用音軌的清單。

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

此函式可傳回目前選取的替代音軌和屬性，例如語言。 還可以提取軌道的自動選擇。

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

此函式會選取要播放的替代音軌。

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
