---
description: 當視頻的DRM元資料被包括在媒體流中時，在播放期間執行驗證。
seo-description: 當視頻的DRM元資料被包括在媒體流中時，在播放期間執行驗證。
seo-title: 播放期間的DRM驗證
title: 播放期間的DRM驗證
uuid: a1a63e3e-be34-49e1-96c4-ae266003b3d1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 播放期間的DRM驗證 {#drm-authentication-during-playback}

當視頻的DRM元資料被包括在媒體流中時，在播放期間執行驗證。

請考慮授權輪換功能，其中資產會使用多份DRM授權加密。 每次發現新的DRM元資料時，使用 `DRMHelper` 方法檢查DRM元資料是否需要DRM驗證。

>[!NOTE]
>
>本教學課程不處理網域系結的授權。 最好是在開始播放之前，先檢查您是否要處理網域系結授權。 如果是，請執行域驗證（如果需要）並加入域。

1. 當在資產中發現新的DRM中繼資料時，會在應用程式層傳送事件。

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. 使用 `DRMMetadata` 檢查是否需要驗證。 如果不能，則不要做；播放繼續不間斷。
1. 否則，請執行DRM驗證。 由於此操作是非同步的，而且是在不同的線程中處理的，因此對用戶介面和視頻播放沒有影響。
1. 如果驗證失敗，使用者就無法繼續檢視視訊，而播放也會停止。 否則，播放將會持續進行。

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
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
