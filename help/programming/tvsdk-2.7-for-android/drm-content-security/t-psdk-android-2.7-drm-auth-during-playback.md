---
description: 當視頻的DRM元資料包含在媒體流中時，可在播放期間執行驗證。
title: 播放期間的DRM驗證
exl-id: f6e6e73a-d455-4b2c-b35c-2db173372092
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 播放期間的DRM驗證 {#drm-authentication-during-playback}

當視頻的DRM元資料包含在媒體流中時，可在播放期間執行驗證。

使用許可輪替，使用多個DRM許可證對資產進行加密。 每次發現新DRM元資料時， `DRMHelper` 方法用於檢查DRM元資料是否需要DRM驗證。

>[!TIP]
>
>在開始播放之前，請確定您是否正在處理域綁定許可證以及是否需要域身份驗證。 如果是，請完成域驗證並加入域。

1. 當在資產中發現新的DRM元資料時，在應用層調度事件。

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

1. 使用 `DRMMetadata` 檢查是否需要驗證。

   * 如果不需要身份驗證，則無需執行任何操作，並且不中斷地繼續播放。
   * 如果需要驗證，請完成DRM驗證。

      由於此操作是非同步的，並且是在其他線程中處理的，因此它不會影響用戶介面或視頻播放。

1. 如果驗證失敗，則用戶無法繼續查看視頻，並停止播放。

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
