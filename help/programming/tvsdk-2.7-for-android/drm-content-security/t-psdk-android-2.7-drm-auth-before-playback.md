---
description: 當視訊的DRM中繼資料與媒體資料流不同時，您應該在開始播放之前進行驗證。
title: 播放前DRM驗證
exl-id: b3267363-f734-44a6-99f5-e155deb53f3e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 播放前DRM驗證 {#drm-authentication-before-playback}

當視訊的DRM中繼資料與媒體資料流不同時，您應該在開始播放之前進行驗證。

視訊資產可以有相關聯的DRM中繼資料檔案，例如：

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

在此範例中，您可以使用 `DRMHelper` 下載DRM中繼資料檔案內容、解析該檔案以及檢查是否需要DRM驗證的方法。

1. 使用 `loadDRMMetadata` 以載入中繼資料URL內容，並將下載的位元組剖析為 `DRMMetadata`.

   >[!TIP]
   >
   >此方法為非同步方法，並建立自己的執行緒。

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

1. 通知使用者此作業為非同步，最好讓使用者知道。

   如果使用者不知道操作為非同步，他們可能會想知道為什麼播放尚未開始。 例如，您可以在下載並剖析DRM中繼資料時顯示旋轉滾輪。

1. 在中實施回呼 `DRMLoadMetadataListener`.

   此 `loadDRMMetadata` 呼叫這些事件處理常式。

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

   以下是有關處理常式的其他詳細資料：

   * `onLoadMetadataUrlStart` 會偵測中繼資料URL載入何時開始。
   * `onLoadMetadataUrlComplete` 會偵測中繼資料URL何時完成載入。
   * `onLoadMetadataUrlError` 表示中繼資料無法載入。

1. 載入完成後，請檢查 `DRMMetadata` 物件來決定是否需要DRM驗證。

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

1. 完成下列其中一項作業：

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

      在此範例中，為了簡單起見，使用者的名稱和密碼會明確編碼：

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

1. 使用事件監聽器來檢查驗證狀態。

   此程式代表網路通訊，因此這也是非同步操作。

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

1. 如果驗證成功，請開始播放。
1. 如果驗證失敗，請通知使用者並且不要開始播放。

   您的應用程式必須處理任何驗證錯誤。 播放前無法成功驗證，導致TVSDK處於錯誤狀態，且播放停止。 您的應用程式必須解決問題、重設播放器，然後重新載入資源。
