---
description: 您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，作為Adobe整合式Primetime DRM解決方案的替代方案。
title: Primetime DRM介面概觀
exl-id: 2f6e50e6-39f0-4939-bb9b-6c46e34bab7e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 概觀 {#primetime-drm-interface-overview}

您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，作為Adobe整合式Primetime DRM解決方案的替代方案。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

請洽詢您的Adobe代表，以取得有關第三方DRM解決方案可用性的最新資訊。

Primetime數位版權管理(DRM)系統的關鍵使用者端元素是DRM管理員。 Android SDK隨附的範例應用程式包含 `DRMHelper` 類別，說明如何讓特定DRM作業更容易實作。

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以為每個數位媒體檔案建立授權，藉此保護和管理視訊內容的許可權。

請參閱TVSDK套件中包含的DRM範例播放器程式碼。

以下是使用DRM時最重要的API元素：

* 在媒體播放器中對實作DRM子系統的DRM管理員物件的參考：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >此API將傳回有效的 `DRMManager` 物件僅位於 `MediaPlayerEvent.DRM_METADATA` 觸發。 如果您呼叫 `getDRMManager()` 觸發此事件之前，可能會傳回NULL。

* 此 `DRMHelper` helper類別，在實作DRM工作流程時很有用。

   您可以看到 `DRMHelper` 在 `ReferencePlayer`.

* A `DRMHelper` 中繼資料載入器方法，當DRM中繼資料位於與媒體不同的獨立URL中時，就會載入中繼資料。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* A `DRMHelper` 檢查DRM中繼資料以確定是否需要驗證的方法。

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

* [com.adobe.ave.drm.DRManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPpolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

如需DRM的詳細資訊，請參閱 [Adobe Primetime DRM檔案](https://helpx.adobe.com/primetime/user-guide.html).
