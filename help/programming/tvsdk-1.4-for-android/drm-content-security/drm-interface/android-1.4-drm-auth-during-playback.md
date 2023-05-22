---
description: 當視頻的DRM元資料被包括在媒體流中時，在回放期間執行驗證。
title: 播放期間的DRM驗證
exl-id: 3f190d37-291e-4a5e-811d-7e9984a6a44a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 播放期間的DRM驗證 {#drm-authentication-during-playback}

當視頻的DRM元資料被包括在媒體流中時，在回放期間執行驗證。

請考慮許可證輪替功能，在該功能中，使用多個DRM許可證對資產進行加密。 每次發現新的DRM元資料時，使用 `DRMHelper` 方法來檢查DRM元資料是否需要DRM驗證。

>[!NOTE]
>
>本教程不處理域綁定的許可證。 理想情況下，在開始播放之前，請檢查您是否正在處理域綁定許可證。 如果是，請執行域身份驗證（如果需要）並加入域。

1. 當在資產中發現新的DRM元資料時，在應用層調度事件。

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

1. 使用 `DRMMetadata` 檢查是否需要驗證。 否則，什麼也不做；播放繼續不間斷。
1. 否則，執行DRM驗證。 由於此操作是非同步的，並且是在其他線程中處理的，因此它不會影響用戶介面或視頻播放。
1. 如果驗證失敗，則用戶無法繼續觀看視頻，並停止播放。 否則，將不間斷地繼續播放。

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
