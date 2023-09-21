---
description: 當視訊的DRM中繼資料包含在媒體串流中時，請在播放期間執行驗證。
title: 錄放期間的DRM驗證
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 錄放期間的DRM驗證 {#drm-authentication-during-playback}

當視訊的DRM中繼資料包含在媒體串流中時，請在播放期間執行驗證。

考慮使用許可證旋轉功能，其中資產使用多個DRM許可證加密。 每次發現新的DRM中繼資料時，請使用 `DRMHelper` 檢查DRM中繼資料是否需要DRM驗證的方法。

>[!NOTE]
>
>本教學課程不處理網域繫結的授權。 理想情況下，在開始播放之前，請檢查您是否正在處理網域繫結的授權。 如果是，請執行網域驗證（如果需要）並加入網域。

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

1. 使用 `DRMMetadata` 以檢查是否需要驗證。 如果沒有，則不執行任何動作；播放作業會繼續不中斷地進行。
1. 否則，請執行DRM驗證。 由於此作業為非同步作業，且是在不同的執行緒中處理，因此對使用者介面或視訊播放均沒有影響。
1. 如果驗證失敗，使用者將無法繼續檢視視訊，而且會停止播放。 否則，播放將持續進行。

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
