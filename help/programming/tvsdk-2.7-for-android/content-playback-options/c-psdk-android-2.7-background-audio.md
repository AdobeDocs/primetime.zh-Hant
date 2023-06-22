---
title: 啟用背景音訊
description: 啟用背景音訊
copied-description: true
exl-id: db494969-ef63-46ad-9f08-a95f58c8b27b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 啟用背景音訊 {#enable-background-audio}

若要在應用程式於背景時啟用音訊播放，應用程式應呼叫 `enableAudioPlaybackInBackground` 當播放器處於已準備狀態時，具有true作為引數的MediaPlayer的API。

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

應用程式在回應電話等事件期間失去音訊焦點保留時，應暫停播放。 下列程式碼片段示範如何實作 `OnAudioFocusChangeListener`：

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
