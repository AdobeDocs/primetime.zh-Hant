---
description: 當視訊的DRM中繼資料與媒體串流分開時，在開始播放之前先執行驗證。
seo-description: 當視訊的DRM中繼資料與媒體串流分開時，在開始播放之前先執行驗證。
seo-title: 播放前的DRM驗證
title: 播放前的DRM驗證
uuid: 326ef93d-53b0-4e3a-b16d-f3b886837cc0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 播放前的DRM驗證 {#drm-authentication-before-playback}

當視訊的DRM中繼資料與媒體串流分開時，在開始播放之前先執行驗證。

視頻資產可以具有相關聯的DRM元資料檔案。 例如：

* 「url」:&quot;<span></span>https://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;:&quot;<span></span>https://www.domain.com/asset.metadata&quot;

在這種情況下，請使 `DRMHelper` 用方法下載DRM元資料檔案的內容，對其進行解析，並檢查是否需要DRM驗證。

1. 使用 `loadDRMMetadata` 以載入中繼資料URL內容，並將下載的位元組剖析為 `DRMMetadata`。

   與任何其他網路操作一樣，此方法是非同步的，建立自己的線程。

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   例如：

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. 由於操作是非同步的，因此最好讓用戶知道。 否則，他會納悶為什麼沒有開始播放。 例如，在下載和解析DRM元資料時顯示旋轉輪。
1. 在中實施回呼 `DRMLoadMetadataListener`。 呼叫 `loadDRMMetadata` 這些事件處理常式（調度這些事件）。

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

   * `onLoadMetadataUrlStart` 偵測中繼資料URL載入何時開始。
   * `onLoadMetadataUrlComplete` 偵測中繼資料URL何時完成載入。
   * `onLoadMetadataUrlError` 表示無法載入中繼資料。

1. 當載入完成時，請檢查 `DRMMetadata` 物件以查看是否需要DRM驗證。

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. 如果不需要驗證，請開始播放。
1. 如果需要驗證，請通過獲取許可證來執行驗證。

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

   為簡單起見，此示例明確為用戶的名稱和密碼編碼。

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   ```

1. 這也意味著網路通信，因此這也是非同步操作。 使用事件偵聽器檢查驗證狀態。

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   ```

1. 如果驗證成功，請開始播放。
1. 如果驗證失敗，請通知使用者並不要開始播放。

您的應用程式必須處理任何驗證錯誤。 無法在播放TVSDK進入錯誤狀態之前成功驗證。 即，它將其狀態更改為ERROR，生成包含來自DRM庫的錯誤代碼的錯誤，並且重放停止。 您的應用程式必須解決問題、重設播放器，並重新載入資源。

