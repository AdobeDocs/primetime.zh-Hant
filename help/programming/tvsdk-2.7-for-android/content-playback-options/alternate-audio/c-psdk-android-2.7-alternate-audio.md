---
description: 替代音效可讓您在視訊音軌的可用音軌間切換。 當視訊播放時，使用者可以選擇偏好的語言軌道。
seo-description: 替代音效可讓您在視訊音軌的可用音軌間切換。 當視訊播放時，使用者可以選擇偏好的語言軌道。
seo-title: 替代音訊
title: 替代音訊
uuid: 86aa5393-6a9e-49db-807b-7299e6b4ab2b
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 概觀 {#alternate-audio-overview}

替代音效可讓您在視訊音軌的可用音軌間切換。 當視訊播放時，使用者可以選擇偏好的語言軌道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立目 `MediaPlayerItem` 前視訊的例項時，會為每個可用 `AudioTrack` 的音軌建立項目。 項目包含屬 `name` 性，屬性是字串，通常包含該追蹤語言的使用者可辨識描述。 項目也包含是否依預設使用該追蹤的資訊。 在播放視訊時，您可以要求提供可用音軌清單、選擇性允許使用者選擇音軌，並設定視訊與選取的音軌一起播放。

>[!TIP]
>
>雖然很少，但若TVSDK建立後有其他音軌可供使用， `MediaPlayerItem`TVSDK會觸發事 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 件。

## 新增API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已新增下列API以支援替代音訊：

`hasAlternateAudio`

如果指定的媒體有替代音軌（除預設音軌外），此布林值函式會傳回 `true`。 如果沒有替代音軌，函式會傳回 `false`。

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

此函式會傳回指定媒體中所有目前可用音軌的清單。

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

此函式可傳回目前選取的替代音軌和屬性，例如語言。 還可以提取軌道的自動選擇。

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

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

