---
title: 授權贏取程式詳細資料
description: 授權贏取程式詳細資料
copied-description: true
exl-id: d772339a-8d05-401b-b5c1-18169b3627b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 授權贏取程式詳細資料 {#license-acquisition-process-details}

此程式提供Primetime DRM受保護內容工作流程的詳細API層級檢視：

1. 使用 `URLLoader` 物件，載入受保護內容的中繼資料檔案的位元組。

   將此物件設定為變數，例如 `metadata_bytes`. Primetime DRM控制的所有內容都有Primetime DRM中繼資料。 封裝內容時，此中繼資料可儲存為單獨的中繼資料檔案( [!DNL .metadata])及內容。 或者，中繼資料可採用Base64編碼，並插入視訊資訊清單檔案的正文中。 如需詳細資訊，請參閱 [正在封裝媒體檔案](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. 如有必要，請移除驚歎號 `!` 從字串的開頭開始。
   1. 如果HLS或HDS內容需要，請先將Base64編碼字串中包含的中繼資料解碼為二進位資料，然後再傳遞它。
1. 建立 `DRMContentData` 執行個體。

   將此程式碼放入try-catch區塊中：

   ```
   new DRMContentData(metadata_bytes)
   ```

   位置 `metadata_bytes` 是 `URLLoader` 在步驟1中取得的物件。

   [iOS： DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android：DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. 建立接聽程式來接聽 `DRMStatusEvent` 和 `DRMErrorEvent` 已從以下位置傳送： `DRMManager` 物件。

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   在 `DRMStatusEvent` 接聽程式，檢查授權是否有效（不是null）。 在 `DRMErrorEvent` 接聽程式，控制代碼 `DRMErrorEvents`. 另請參閱 *使用DRMStatusEvent類別* 和 *使用DRMErrorEvent類別* 在本指南中。

1. 載入播放內容所需的授權。
首先，嘗試載入本機儲存的授權以播放內容：

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android： DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS： acquireLicense：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   載入完成後， `DRMManager` 物件傳送次數 `DRMStatusEvent.DRM_Status`.

1. 檢查 `DRMVoucher` 物件。


   如果 `DRMVoucher` 物件不是null，授權有效。 前往步驟9。

   [Android： DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS： DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. 檢查此內容的原則所需的驗證方法。

   使用 `DRMContentData.authenticationMethod` 屬性。
   1. 如果驗證方法為 `ANONYMOUS`，請前往步驟9。 

      [Android：DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS： DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. 如果驗證方法為 `USERNAME_AND_PASSWORD`，您的應用程式必須提供讓使用者輸入認證的機制。

      將使用者的認證傳遞至授權伺服器以驗證使用者：

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      此 `DRMManager` 傳送 `DRMAuthenticationErrorEvent` 如果驗證失敗，或 `DRMAuthenticationCompleteEvent` 如果驗證成功。 為這些事件建立接聽程式。

      [Android： authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS：驗證：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe建議使用更安全的機制來提供認證。 如需參考資訊，請參閱 [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. 如果驗證方法為 `UNKNOWN`，您必須使用自訂驗證方法。

      在此情況下，內容提供者已安排以頻外方式完成驗證，而不是使用Primetime API。 自訂驗證程式必須產生可傳遞至的驗證權杖 `DRMManager.setAuthenticationToken()` 方法。

      [Android： setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[]，%20com.adobe.ave.drm.DRMOperationErrorCallback，%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS： setAuthenticationToken：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >或者，無論驗證方法為何， `.setAuthenticationToken()` 可用來將自訂資料從使用者端傳送至授權伺服器。 這是API的過載，因為此機制是在取得授權時，從使用者端傳送動態自訂資料到授權伺服器的唯一方法。 此自訂資料傳輸方法會在的多篇論壇文章中深入討論，位置如下： [Primetime DRM (Adobe存取)論壇 ](https://forums.adobe.com/community/adobe_access).

1. 如果驗證失敗，您的應用程式必須返回步驟6。

   確保您的應用程式具備處理並限制重複驗證失敗的機制。 例如，在第三次嘗試後，您向使用者顯示一則訊息，指出驗證失敗且無法播放內容。
1. 若要使用儲存的權杖而不提示使用者輸入認證，請使用以下專案設定權杖： `DRMManager.setAuthenticationToken()` 方法。

   然後，您會從授權伺服器下載授權，並播放內容，如步驟6所示。
   1. **可選：** 如果驗證成功，您可以擷取驗證Token，這是在記憶體中快取的位元組陣列。

      使用取得此Token `DRMAuthenticationCompleteEvent.token` 屬性。 您可以儲存和使用驗證Token，讓使用者不必重複輸入此內容的認證。 授權伺服器會決定驗證Token的有效期間。

      [Android： OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS： DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. 如果驗證成功，請從授權伺服器下載授權：

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   載入完成後， `DRMManager` 物件傳送次數 `DRMStatusEvent.DRM_STATUS`. 接聽此事件，並在傳送時播放內容。  透過建立Primetime物件然後呼叫它來播放視訊 `play()` 方法：

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android： acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS： acquireLicense：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)
