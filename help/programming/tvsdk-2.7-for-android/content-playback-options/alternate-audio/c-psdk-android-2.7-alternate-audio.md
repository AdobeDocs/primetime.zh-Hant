---
description: 備用音頻允許您在視頻軌道的可用音頻軌道之間切換。 用戶可以在播放視頻時選擇其首選語言軌道。
title: 備用音頻
exl-id: c2eb10dc-3fe0-472b-8450-2fbfc6b09487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 概述 {#alternate-audio-overview}

備用音頻允許您在視頻軌道的可用音頻軌道之間切換。 用戶可以在播放視頻時選擇其首選語言軌道。

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

當TVSDK建立 `MediaPlayerItem` 當前視頻的實例，將建立 `AudioTrack` 每個可用音頻軌道的項目。 該項包含 `name` 屬性，該字串通常包含該軌道語言的用戶可識別的描述。 該項目還包含有關是否預設使用該跟蹤的資訊。 播放視頻時，您可以要求提供可用音頻軌道的清單，或者允許用戶選擇一個軌道，並設定視頻以與所選軌道一起播放。

>[!TIP]
>
>雖然很少，但如果TVSDK建立後有附加的音頻軌道可用 `MediaPlayerItem`,TVSDK將觸發 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 的子菜單。

## 添加的API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

已添加以下API以支援備用音頻：

`hasAlternateAudio`

如果指定的介質具有備用音頻軌道（預設軌道除外），則此布爾函式將返回 `true`。 如果沒有備用音頻軌道，則函式返回 `false`。

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

此函式返回指定介質中所有當前可用音頻軌道的清單。

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

此函式返回當前選擇的備用音頻軌道和屬性（如語言）。 還可以提取軌跡的自動選擇。

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

此函式選擇要播放的備用音頻軌道。

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
