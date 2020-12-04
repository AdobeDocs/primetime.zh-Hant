---
description: 您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，做為Adobe整合Primetime DRM解決方案的替代方案。
seo-description: 您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，做為Adobe整合Primetime DRM解決方案的替代方案。
seo-title: Primetime DRM介面總覽
title: Primetime DRM介面總覽
uuid: 71479464-8356-4732-9774-da9f6084e6ad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# 概述{#primetime-drm-interface-overview}

您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，做為Adobe整合Primetime DRM解決方案的替代方案。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

請洽詢您的Adobe代表，以取得有關協力廠商DRM解決方案可用性的最新資訊。

Primetime數位版權管理(DRM)系統的主要用戶端元素是DRM管理器。 Android SDK隨附的範例應用程式包含`DRMHelper`類別，示範如何讓某些DRM作業更容易實作。

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以針對每個數位媒體檔案建立授權，以保護並管理視訊內容的權利。

請參閱TVSDK套件中包含的DRM範例播放器程式碼。

以下是使用DRM時最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的參考：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >此API只有在`MediaPlayerEvent.DRM_METADATA`引發後才會傳回有效的`DRMManager`物件。 如果您在觸發此事件之前呼叫`getDRMManager()`，則可能會傳回NULL。

* `DRMHelper`幫助類，在實施DRM工作流時非常有用。

   您可在`ReferencePlayer`中看到`DRMHelper`。

* `DRMHelper`中繼資料載入器方法，當DRM中繼資料位於與媒體不同的URL時，會載入該方法。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* 一種檢查DRM元資料以確定是否需要驗證的`DRMHelper`方法。

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

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

其他相關API元素：

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

如需DRM的詳細資訊，請參閱[Adobe Primetime DRM檔案](https://helpx.adobe.com/primetime/user-guide.html)。
