---
description: 當視訊的DRM中繼資料包含在媒體串流中時，您可以在播放期間執行驗證。
title: 播放期間的DRM驗證
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---


# 播放{#drm-authentication-during-playback}期間的DRM驗證

當視訊的DRM中繼資料包含在媒體串流中時，您可以在播放期間執行驗證。

透過授權輪換，資產會使用多份DRM授權加密。 每次發現新的DRM元資料時，`DRMHelper`方法被用來檢查DRM元資料是否需要DRM驗證。

>[!TIP]
>
>在開始播放之前，請確定您是否處理網域系結授權，以及是否需要網域驗證。 如果是，請完成域驗證並加入域。

1. 在資產中發現新的DRM中繼資料時，會在應用程式層傳送事件。

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. 使用`DRMMetadata`檢查是否需要驗證。

   * 如果不需要驗證，則您不需要執行任何動作，而且播放會持續不中斷。
   * 如果需要驗證，請完成DRM驗證。

      由於此操作是非同步的，而且是在不同的線程中處理的，因此對用戶介面和視頻播放沒有影響。

1. 如果驗證失敗，使用者就無法繼續檢視視訊，而播放會停止。

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

例如：

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
 
        }); 
    } 
}; 
```
