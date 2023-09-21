---
description: 當視訊的DRM中繼資料包含在媒體串流中時，您可以在播放期間執行驗證。
title: 錄放期間的DRM驗證
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 錄放期間的DRM驗證 {#drm-authentication-during-playback}

當視訊的DRM中繼資料包含在媒體串流中時，您可以在播放期間執行驗證。

使用授權輪換時，資產會使用多個DRM授權加密。 每次發現新的DRM中繼資料時， `DRMHelper` 方法可用來檢查DRM中繼資料是否需要DRM驗證。

>[!TIP]
>
>在開始播放之前，請判斷您是否要處理網域繫結的授權，以及是否需要網域驗證。 如果是，請完成網域驗證並加入網域。

1. 當在資產中發現新的DRM中繼資料時，會在應用程式層傳送事件。

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

1. 使用 `DRMMetadata` 以檢查是否需要驗證。

   * 如果不需要驗證，您就不需要執行任何動作，而且播放作業會繼續不中斷地進行。
   * 如果需要驗證，請完成DRM驗證。

     由於此作業為非同步作業，且是在不同的執行緒中處理，因此對使用者介面或視訊播放均沒有影響。

1. 如果驗證失敗，使用者將無法繼續檢視視訊，且播放會停止。

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
