---
description: 該黃金時段播放器支援黃金時段DRM整合作為自定義DRM工作流。 這意味著您的應用程式必須在播放流之前實施DRM驗證工作流。
title: DRM內容保護
exl-id: c1904d15-023f-49fb-95f9-d157d17b3516
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# DRM內容保護 {#drm-content-protection}

該黃金時段播放器支援黃金時段DRM整合作為自定義DRM工作流。 這意味著您的應用程式必須在播放流之前實施DRM驗證工作流。

要啟用此功能，TVSDK會為您提供DRM管理器進行身份驗證。 參考實現提供了以下工作流的示例：

* 如何通過Access內容保護載入和回放HLS流，並針對低錯誤率和快速啟動進行了優化。
* 如何使用AES128內容保護載入和回放HLS流。
* 如何通過PHLS內容保護載入和回放HLS流，並針對低錯誤率和快速啟動進行了優化。

所有受DRM保護的內容都由TVSDK中內置的DRM庫自動處理。 但是，您可以使用TVSDK API回調來公開錯誤處理、設備個性化優化和許可證獲取。

## 向播放器添加內容保護 {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

可以通過建立播放管理器或使用管理器工廠將內容保護添加到播放器。

要建立內容保護管理器：

* 初始化DRM系統。

   以下代碼示例顯示調用 `loadDRMServices` 在 `onCreate()` 功能，以確保在重放開始之前啟動DRM系統所需的任何初始化。

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* 預載入DRM許可證。

   以下代碼示例顯示載入 `VideoItems` 內容清單載入完畢後。 這將導致從許可證伺服器獲取DRM許可證並在本地快取，因此當播放開始時，內容將以最小延遲載入。

   ```java
   DrmManager.preLoadDrmLicenses(item.getUrl(),  
     new MediaPlayerItemLoader.LoaderListener() { 
   
       @Override 
       public void onLoadComplete(MediaPlayerItem item) { 
           Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
       } 
   
       @Override 
       public void onError(MediaErrorCode errorCode, String s) { 
           Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
       } 
   } 
   ```

   >[!NOTE]
   >
   >可以在「設定」用戶介面中將「預快取DRM許可證」設定為「開啟」，以便在載入內容時預快取DRM許可證。 但是，最佳做法是預載入特定項目，而不是預先刪除目錄中的所有許可證。
   >
   >![](assets/precache-drm-licenses.jpg)

* 要使用 `ManagerFactory` 要實現DRM錯誤處理，請確保以下代碼行位於 [!DNL PlayerFragment.java] 檔案：

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**相關API文檔**

* [類DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
