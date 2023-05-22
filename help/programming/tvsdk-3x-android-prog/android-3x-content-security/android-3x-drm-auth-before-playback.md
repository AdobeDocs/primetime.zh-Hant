---
description: 當視頻的DRM元資料與媒體流分開時，應在開始播放之前進行身份驗證。
title: 播放前DRM驗證
exl-id: 74eb7218-403e-4264-9063-bf959403436f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 播放前DRM驗證 {#drm-authentication-before-playback}

當視頻的DRM元資料與媒體流分開時，應在開始播放之前進行身份驗證。

視頻資產可以具有關聯的DRM元資料檔案，例如：

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

在此示例中，您可以 `DRMHelper` 方法下載DRM元資料檔案的內容、分析它並檢查是否需要DRM驗證。

1. 使用 `loadDRMMetadata` 載入元資料URL內容並將下載的位元組解析到 `DRMMetadata`。

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

1. 通知用戶此操作是非同步的，最好讓用戶知道這一點。

   如果用戶不知道該操作是非同步的，他們可能會想知道為什麼尚未開始播放。 例如，在下載和分析DRM元資料時，可以顯示旋轉輪。

1. 在 `DRMLoadMetadataListener`。

   的 `loadDRMMetadata` 調用這些事件處理程式。

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

   以下是有關處理程式的其他詳細資訊：

   * `onLoadMetadataUrlStart` 檢測元資料URL載入何時開始。
   * `onLoadMetadataUrlComplete` 檢測元資料URL何時完成載入。
   * `onLoadMetadataUrlError` 指示載入元資料失敗。

1. 載入完成後，檢查 `DRMMetadata` 確定是否需要DRM驗證。

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

1. 完成以下任務之一：

   * 如果不需要驗證，請開始播放。
   * 如果需要驗證，請通過獲取許可證來完成驗證。

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

      在本示例中，為了簡單起見，用戶的名稱和口令被顯式編碼：

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

   這個過程意味著網路通信，因此這也是一個非同步操作。

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
1. 如果驗證失敗，請通知用戶，並且不要開始播放。

   您的應用程式必須處理任何身份驗證錯誤。 在播放TVSDK進入錯誤狀態之前未能成功進行身份驗證，播放將停止。 您的應用程式必須解決問題，重置播放器並重新載入資源。
