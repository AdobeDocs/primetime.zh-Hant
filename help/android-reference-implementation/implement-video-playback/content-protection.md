---
description: Primetime播放器支援Primetime DRM整合作為自訂DRM工作流程。 這表示您的應用程式必須先實作DRM驗證工作流程，才能播放資料流。
title: DRM內容保護
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# DRM內容保護 {#drm-content-protection}

Primetime播放器支援Primetime DRM整合作為自訂DRM工作流程。 這表示您的應用程式必須先實作DRM驗證工作流程，才能播放資料流。

若要啟用此功能，TVSDK會提供DRM管理員以進行驗證。 參考實作提供下列工作流程的範例：

* 如何載入及播放具有Access內容保護的HLS資料流，針對低錯誤率和快速啟動進行最佳化。
* 如何使用AES128內容保護來載入及播放HLS資料流。
* 如何載入及播放具有PHLS內容保護的HLS資料流，針對低錯誤率和快速啟動進行最佳化。

所有受DRM保護的內容都會由內建在TVSDK中的DRM資料庫自動處理。 不過，您可以使用TVSDK API回呼，公開錯誤處理、裝置個人化最佳化和授權贏取。

## 為播放器新增內容保護 {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

您可以建立播放管理員或使用管理員處理站，將內容保護新增至播放器。

若要建立內容保護管理員：

* 初始化DRM系統。

  下列程式碼範例顯示呼叫 `loadDRMServices` 在應用程式中 `onCreate()` 函式，以確保在開始播放之前先啟動DRM系統所需的任何初始化。

  ```java
  @Override 
   public void onCreate() { 
       super.onCreate();  
       DrmManager.loadDRMServices(getApplicationContext()); 
   }
  ```

* 預先載入DRM授權。

  下列程式碼範例說明如何載入 `VideoItems` 內容清單載入完成後。 這將導致DRM許可證從許可證伺服器取得並在本機快取，因此當播放開始時，內容將以最小的延遲載入。

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
  >您可以在「設定」使用者介面中將Precache DRM授權設定為ON，以便在載入內容時預先快取DRM授權。 不過，最佳實務是預先載入特定專案，而非預先載入目錄中的所有授權。
  >
  >![](assets/precache-drm-licenses.jpg)

* 使用 `ManagerFactory` 若要實作DRM錯誤處理，請確定下列程式碼行位於 [!DNL PlayerFragment.java] 檔案：

  ```java
  drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
  ```

**相關API檔案**

* [類別DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
