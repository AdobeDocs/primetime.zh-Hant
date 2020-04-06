---
description: 當視訊的DRM中繼資料與媒體串流分開時，您應在開始播放之前先進行驗證。
seo-description: 當視訊的DRM中繼資料與媒體串流分開時，您應在開始播放之前先進行驗證。
seo-title: 播放前的DRM驗證
title: 播放前的DRM驗證
uuid: be319b04-a506-4278-8275-db32cd3f18aa
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 播放前的DRM驗證 {#drm-authentication-before-playback}

當視訊的DRM中繼資料與媒體串流分開時，您應在開始播放之前先進行驗證。

視訊資產可以具有關聯的DRM中繼資料檔案，例如：

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

在此示例中，您可以使 `DRMHelper` 用方法下載DRM元資料檔案的內容、對其進行解析，並檢查是否需要DRM驗證。

1. 使用 `loadDRMMetadata` 以載入中繼資料URL內容，並將下載的位元組剖析為 `DRMMetadata`。

   >[!TIP]
   >
   >此方法是非同步的，並建立其自己的線程。

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   例如：

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. 通知用戶此操作是非同步的，建議用戶注意此操作。

   如果使用者不知道此作業是非同步的，他們可能會想知道為什麼尚未開始播放。 例如，當下載和解析DRM元資料時，可以顯示旋轉輪。

1. 在中實施回呼 `DRMLoadMetadataListener`。

   `loadDRMMetadata`會呼叫這些事件處理常式。

   ```java
   public interface DRMLoadMetadataListener { 
    
       public void onLoadMetadataUrlStart(); 
    
       /** 
       * @param authNeeded 
       * whether DRM authentication is needed. 
       * @param drmMetadata 
       * the parsed DRMMetadata obtained.    */ 
       public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata); 
       public void onLoadMetadataUrlError(); 
   } 
   
   ```   

   程式的其他詳細資訊：

   * `onLoadMetadataUrlStart` 偵測中繼資料URL載入何時開始。
   * `onLoadMetadataUrlComplete` 偵測中繼資料URL何時完成載入。
   * `onLoadMetadataUrlError` 表示無法載入中繼資料。

1. 載入完成後，請檢查物 `DRMMetadata` 件以判斷是否需要DRM驗證。

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   例如：

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. 完成下列任務之一：

   * 如果不需要驗證，請開始播放。
   * 如果需要驗證，請取得授權以完成驗證。

      ```java
      /** 
      * Helper method to perform DRM authentication. 
      * 
      * @param drmManager 
      * the DRMManager, used to perform the authentication. 
      * @param drmMetadata 
      * the DRMMetadata, containing the DRM specific information. 
      * @param authenticationListener 
      * the listener, on which the user can be notified about the 
      * authentication process status. 
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      在此示例中，為了簡單起見，用戶的名稱和口令被顯式編碼：

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. 使用事件偵聽器檢查驗證狀態。

   這個過程意味著網路通信，因此這也是非同步操作。

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. 如果驗證成功，請啟動播放。
1. 如果驗證失敗，請通知使用者並不要開始播放。

   您的應用程式必須處理任何驗證錯誤。 播放將TVSDK置於錯誤狀態前無法成功驗證，而播放會停止。 您的應用程式必須解決問題、重設播放器，並重新載入資源。
