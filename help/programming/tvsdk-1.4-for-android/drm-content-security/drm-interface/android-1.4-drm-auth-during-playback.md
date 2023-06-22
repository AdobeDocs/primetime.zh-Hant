---
description: 當視訊的DRM中繼資料包含在媒體串流中時，請在播放期間執行驗證。
title: 在播放期間DRM驗證
exl-id: 3f190d37-291e-4a5e-811d-7e9984a6a44a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 在播放期間DRM驗證 {#drm-authentication-during-playback}

當視訊的DRM中繼資料包含在媒體串流中時，請在播放期間執行驗證。

考慮使用授權輪換功能，其中資產會使用多個DRM授權進行加密。 每次發現新的DRM中繼資料時，請使用 `DRMHelper` 檢查DRM中繼資料是否需要DRM驗證的方法。

>[!NOTE]
>
>本教學課程不處理網域繫結的授權。 理想情況下，在開始播放之前，請檢查您是否正在處理領域繫結的授權。 如果是，請執行網域驗證（如果需要）並加入網域。

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

1. 使用 `DRMMetadata` 以檢查是否需要驗證。 如果不會，則不執行任何動作；播放會持續不中斷。
1. 否則，請執行DRM驗證。 由於此作業為非同步作業，且在不同執行緒中處理，因此對使用者介面或視訊播放均無影響。
1. 如果驗證失敗，使用者將無法繼續檢視視訊，且播放會停止。 否則，播放將持續進行。

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
