---
description: Primetime播放器支援將Primetime DRM整合為自訂DRM工作流程。 這表示您的應用程式必須在播放串流之前，先實作DRM驗證工作流程。
seo-description: Primetime播放器支援將Primetime DRM整合為自訂DRM工作流程。 這表示您的應用程式必須在播放串流之前，先實作DRM驗證工作流程。
seo-title: DRM內容保護
title: DRM內容保護
uuid: 95c446f6-8304-4d70-9bef-7368b9364025
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# DRM內容保護 {#drm-content-protection}

Primetime播放器支援將Primetime DRM整合為自訂DRM工作流程。 這表示您的應用程式必須在播放串流之前，先實作DRM驗證工作流程。

若要啟用此功能，TVSDK會提供DRM管理員以進行驗證。 參考實作提供下列工作流程的範例：

* 如何使用存取內容保護來載入和播放HLS串流，並針對低錯誤率和快速啟動進行最佳化。
* 如何使用AES128內容保護來載入和播放HLS串流。
* 如何使用PHLS內容保護來載入和播放HLS串流，並針對低錯誤率進行最佳化並快速啟動。

所有受DRM保護的內容都會由TVSDK內建的DRM程式庫自動處理。 不過，您可以使用TVSDK API回呼來公開錯誤處理、裝置個人化最佳化和授權取得。

## 為播放器新增內容保護 {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

您可以建立播放管理員或使用管理員工廠，為播放器新增內容保護。

要建立內容保護管理器：

* 初始化DRM系統。

   下面的代碼示例顯示在應 `loadDRMServices` 用程式功 `onCreate()` 能中的調用，以確保在播放開始之前啟動DRM系統所需的任何初始化。

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* 預先載入DRM授權。

   下列程式碼範例顯示內容清 `VideoItems` 單載入完成時的載入。 這會導致從授權伺服器取得DRM授權並在本機快取，如此當播放開始時，內容會以最小延遲載入。

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
   >您可以在「設定」使用者介面中將Precache DRM授權設為「開啟」，以便在載入內容時預先取得DRM授權。 不過，最佳實務是預先載入特定項目，而非預先預先存取目錄中的所有授權。
   >
   >![](assets/precache-drm-licenses.jpg)

* 若要用 `ManagerFactory` 於實作DRM錯誤處理，請確定檔案中有下列程式碼 [!DNL PlayerFragment.java] 行：

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**相關API檔案**

* [類別DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)