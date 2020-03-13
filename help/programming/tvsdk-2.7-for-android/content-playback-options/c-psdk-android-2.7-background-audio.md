---
seo-title: 啟用背景音訊
title: 啟用背景音訊
uuid: 1e7319f5-ee16-47bd-bfd5-d3dcfe69bf4b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 啟用背景音訊 {#enable-background-audio}

若要在應用程式在背景時啟用音訊播放，應用程式應在播放程式處於「已準備」狀態時，以true為引數呼叫MediaPlayer的 `enableAudioPlaybackInBackground` API。

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

當應用程式在回應手機等事件期間失去對音訊焦點的控制時，應該暫停播放。 下列程式碼片段示範如何實作 `OnAudioFocusChangeListener`:

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

