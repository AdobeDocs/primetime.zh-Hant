---
description: Primetime DRM解決方案的關鍵使用者端元素是DRM管理員。 Android SDK隨附的範例應用程式也包含DRMHelper類別，可用來讓特定DRM作業更容易實作。
title: Primetime DRM介面概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Primetime DRM介面概述 {#primetime-drm-interface-overview}

Primetime DRM解決方案的關鍵使用者端元素是DRM管理員。 Android SDK隨附的範例應用程式也包含 `DRMHelper` 可用來讓特定DRM作業更容易實施的類別。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以為每個數位媒體檔案建立授權，以保護和管理視訊內容的許可權。

如需詳細資訊，請參閱TVSDK套件中包含的DRM範例播放器程式碼。

以下是使用DRM時最重要的API元素：

* 在媒體播放器中，對實作DRM子系統的DRM管理員物件的參照：

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >此API將傳回有效的 `DRMManager` 物件僅在 `MediaPlayerEvent.DRM_METADATA` 觸發。 如果您呼叫 `getDRMManager()` 觸發此事件之前，它可能會傳回NULL。

* 此 `DRMHelper` helper類別，在實作DRM工作流程時很有用。
* A `DRMHelper` 中繼資料載入器方法，當DRM中繼資料位於與媒體不同的URL中時，就會載入該中繼資料。

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` 檢查DRM中繼資料並確定是否需要驗證的方法。

  ```java
  /** 
  * Return whether authentication is needed for the provided 
  * DRMMetadata. 
  * 
  * @param drmMetadata 
  * The desired DRMMetadata on which to check whether auth is needed. 
  * @return whether authentication is required for the provided metadata 
  */ 
  public static boolean isAuthNeeded(DRMMetadata drmMetadata);
  ```

* `DRMHelper` 執行驗證的方法。

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
  * @param authUser 
  * the DRM username provider by the user. 
  * @param authPass 
  * the DRM password provided by the user. 
  */ 
  public static void performDrmAuthentication(final DRMManager drmManager,  
  final DRMMetadata drmMetadata,  
  final String authUser,  
  final String authPass,  
  final DRMAuthenticationListener authenticationListener);
  ```

* 通知應用程式各種DRM活動和狀態的事件。

如需有關DRM的詳細資訊，請參閱 [DRM檔案](https://helpx.adobe.com/primetime/user-guide.html).
