---
description: 您可以使用黃金時段Digital Rights Management(DRM)系統的功能來提供對視頻內容的安全訪問。 或者，您可以使用第三方DRM解決方案作為Adobe整合的Mighine DRM解決方案的替代方案。
title: 黃金時段DRM介面概述
exl-id: 2f6e50e6-39f0-4939-bb9b-6c46e34bab7e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 概述 {#primetime-drm-interface-overview}

您可以使用黃金時段Digital Rights Management(DRM)系統的功能來提供對視頻內容的安全訪問。 或者，您可以使用第三方DRM解決方案作為Adobe整合的Mighine DRM解決方案的替代方案。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

請咨詢您的Adobe代表，瞭解有關第三方DRM解決方案可用性的最新資訊。

黃金時段數字版權管理(DRM)系統的關鍵客戶端元素是DRM管理器。 Android SDK附帶的示例應用程式套件括 `DRMHelper` 演示如何使某些DRM操作更容易實現的類。

黃金時段DRM提供可擴展的、高效的工作流，以在TVSDK應用程式中實施內容保護。 通過為每個數字媒體檔案建立許可證，您可以保護和管理視頻內容的權限。

請參閱TVSDK包中包含的DRM示例播放器代碼。

以下是使用DRM的最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的引用：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >此API將返回有效 `DRMManager` 對象僅在 `MediaPlayerEvent.DRM_METADATA` 被炒了。 如果你打電話 `getDRMManager()` 在觸發此事件之前，它可能返回NULL。

* 的 `DRMHelper` 幫助類，在實施DRM工作流時非常有用。

   你可以看到 `DRMHelper` 在 `ReferencePlayer`。

* A `DRMHelper` 元資料載入器方法，當DRM元資料位於與媒體分開的URL中時，該方法載入DRM元資料。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* A `DRMHelper` 方法檢查DRM元資料以確定是否需要驗證。

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

* `DRMHelper` 執行身份驗證的方法。

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
* [com.adobe.ave.drm.DRMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMA認證完整回調](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有關DRM的詳細資訊，請參見 [Adobe PrimetimeDRM文檔](https://helpx.adobe.com/primetime/user-guide.html)。
