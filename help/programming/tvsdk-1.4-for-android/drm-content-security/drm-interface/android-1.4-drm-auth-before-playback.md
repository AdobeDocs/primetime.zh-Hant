---
description: 當視訊的DRM中繼資料與媒體資料流不同時，請在開始播放之前執行驗證。
title: 播放前DRM驗證
exl-id: da81ec38-ea77-4fcd-a6e4-5804465385cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 播放前DRM驗證 {#drm-authentication-before-playback}

當視訊的DRM中繼資料與媒體資料流不同時，請在開始播放之前執行驗證。

視訊資產可以有相關聯的DRM中繼資料檔案。 例如：

* &quot;url&quot;： &quot;ht<span></span>tps://www.domain.com/asset.m3u8」
* &quot;drmMetadata&quot;： &quot;ht<span></span>tps://www.domain.com/asset.metadata」

如果是這種情況，請使用 `DRMHelper` 下載DRM中繼資料檔案內容、解析該檔案以及檢查是否需要DRM驗證的方法。

1. 使用 `loadDRMMetadata` 以載入中繼資料URL內容，並將下載的位元組剖析為 `DRMMetadata`.

   如同任何其他網路操作，此方法為非同步，建立自己的執行緒。

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

1. 由於操作不同步，因此最好讓使用者意識到這一點。 否則，他將會想知道為什麼他的播放沒有開始。 例如，在下載並剖析DRM中繼資料時顯示旋轉滾輪。
1. 在中實施回呼 `DRMLoadMetadataListener`. 此 `loadDRMMetadata` 呼叫這些事件處理常式（排程這些事件）。

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

   * `onLoadMetadataUrlStart` 會偵測中繼資料URL載入何時開始。
   * `onLoadMetadataUrlComplete` 會偵測中繼資料URL何時完成載入。
   * `onLoadMetadataUrlError` 表示中繼資料無法載入。

1. 載入完成時，請檢查 `DRMMetadata` 物件，以檢視是否需要DRM驗證。

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
1. 如果需要驗證，請透過取得授權來執行驗證。

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

   為了簡單起見，此範例明確編碼使用者的名稱和密碼。

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

1. 這也代表網路通訊，因此這也是非同步操作。 使用事件監聽器來檢查驗證狀態。

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
1. 如果驗證失敗，請通知使用者並且不要開始播放。

您的應用程式必須處理任何驗證錯誤。 播放前無法成功驗證，導致TVSDK進入錯誤狀態。 也就是說，它會將其狀態變更為ERROR，產生包含DRM程式庫錯誤代碼的錯誤，然後播放停止。 您的應用程式必須解決問題、重設播放器，然後重新載入資源。
