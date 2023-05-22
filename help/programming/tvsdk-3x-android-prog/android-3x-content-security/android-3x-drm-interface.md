---
description: 黃金時段DRM解決方案的關鍵客戶端元素是DRM管理器。 Android SDK附帶的示例應用程式還包括DRMHelper類，該類可用於使某些DRM操作更容易實現。
title: 黃金時段DRM介面概述
exl-id: 39e9f2e2-0945-4a89-baee-a2e558f03fd4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 黃金時段DRM介面概述 {#primetime-drm-interface-overview}

黃金時段DRM解決方案的關鍵客戶端元素是DRM管理器。 Android SDK附帶的示例應用程式還包括 `DRMHelper` 類，可用於使某些DRM操作更容易實現。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

黃金時段DRM提供可擴展的、高效的工作流，以在TVSDK應用程式中實施內容保護。 通過為每個數字媒體檔案建立許可證，您可以保護和管理視頻內容的權限。

有關詳細資訊，請參閱TVSDK包中包含的DRM示例播放器代碼。

以下是使用DRM時最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的引用：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >此API將返回有效 `DRMManager` 對象僅在 `MediaPlayerEvent.DRM_METADATA` 被炒了。 如果你打電話 `getDRMManager()` 在觸發此事件之前，它可能返回NULL。

* 的 `DRMHelper` 幫助類，在實施DRM工作流時非常有用。
* A `DRMHelper` 元資料載入器方法，當DRM元資料位於與媒體分開的URL中時，該方法載入DRM元資料。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* A `DRMHelper` 方法檢查DRM元資料並確定是否需要驗證。

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

有關DRM的詳細資訊，請參見 [DRM文檔](https://helpx.adobe.com/primetime/user-guide.html)。
