---
title: 啟用後台音頻
description: 啟用後台音頻
copied-description: true
exl-id: 5bb72233-27d0-4968-b32c-c8d5ac5ac8c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 啟用後台音頻 {#enable-background-audio}

要在應用程式處於後台時啟用音頻播放，應用應該呼叫 `enableAudioPlaybackInBackground` 當播放器處於PREPARED狀態時，參數為true的MediaPlayer的API。

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

在響應電話等事件期間，當應用程式失去對音頻焦點的控制時，應暫停播放。 以下代碼段演示了如何實現 `OnAudioFocusChangeListener`:

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
