---
description: 當視頻的DRM元資料與媒體流分離時，在開始回放之前執行驗證。
title: 播放前DRM驗證
exl-id: da81ec38-ea77-4fcd-a6e4-5804465385cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 播放前DRM驗證 {#drm-authentication-before-playback}

當視頻的DRM元資料與媒體流分離時，在開始回放之前執行驗證。

視頻資產可以具有關聯的DRM元資料檔案。 例如：

* &quot;url&quot;:&quot;ht&quot;<span></span>tps://www.domain.com/asset.m3u8
* &quot;drmMetadata&quot;:&quot;ht&quot;<span></span>tps://www.domain.com/asset.metadata

在這種情況下，使用 `DRMHelper` 方法下載DRM元資料檔案的內容、分析它並檢查是否需要DRM驗證。

1. 使用 `loadDRMMetadata` 載入元資料URL內容並將下載的位元組解析到 `DRMMetadata`。

   與任何其他網路操作一樣，此方法是非同步的，它建立了自己的線程。

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

1. 由於操作是非同步的，因此最好讓用戶意識到這一點。 否則，他會想，為什麼他的回放沒有開始。 例如，在下載和分析DRM元資料時顯示旋轉輪。
1. 在 `DRMLoadMetadataListener`。 的 `loadDRMMetadata` 調用這些事件處理程式（調度這些事件）。

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

   * `onLoadMetadataUrlStart` 檢測元資料URL載入何時開始。
   * `onLoadMetadataUrlComplete` 檢測元資料URL何時完成載入。
   * `onLoadMetadataUrlError` 指示載入元資料失敗。

1. 載入完成時，檢查 `DRMMetadata` 查看是否需要DRM驗證。

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

   為簡單起見，此示例顯式地編碼用戶的名稱和密碼。

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
1. 如果驗證失敗，請通知用戶，並且不要開始播放。

您的應用程式必須處理任何身份驗證錯誤。 在將TVSDK置於錯誤狀態之前未能成功驗證。 即，它將其狀態更改為ERROR，生成包含來自DRM庫的錯誤代碼的錯誤，並停止回放。 您的應用程式必須解決問題，重置播放器並重新載入資源。
