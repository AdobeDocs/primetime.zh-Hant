---
seo-title: 授權取得程式詳細資訊
title: 授權取得程式詳細資訊
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# 授權取得程式詳細資訊 {#license-acquisition-process-details}

此程式提供Primetime DRM保護內容工作流程的詳細API層級檢視：

1. 使用物 `URLLoader` 件，載入受保護內容的中繼資料檔案的位元組。

   將此物件設為變數，例如 `metadata_bytes`。 所有由Primetime DRM控制的內容都具有Primetime DRM元資料。 在封裝內容時，此中繼資料可儲存為內容旁的個別中繼資料檔案( [!DNL .metadata])。 或者，元資料可以是Base64編碼的，並插入到視頻清單檔案的主體中。 如需詳細資訊，請參 [閱封裝媒體檔案](../protecting-content/packaging-media-overview/packaging-media-files.md)。
   1. 如有必要，請從字串 `!` 的開頭刪除驚嘆號。
   1. 如果HLS或HDS內容需要，請將Base64編碼字串中包含的中繼資料解碼為二進位資料，然後再傳遞。
1. 建立例 `DRMContentData` 項。

   將此程式碼放入try-catch區塊：

   ```
   new DRMContentData(metadata_bytes)
   ```

   其中 `metadata_bytes` 是在 `URLLoader` 步驟1中獲得的對象。

   [iOS:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. 建立偵聽器以監聽 `DRMStatusEvent` 對象 `DRMErrorEvent` 並從對象調 `DRMManager` 度。

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   在監聽 `DRMStatusEvent` 器中，檢查許可證是否有效（非空）。 在監聽 `DRMErrorEvent` 器中，句柄 `DRMErrorEvents`。 請參 *閱本指南中的「使用DRMStatusEvent類**別和使用DRMErrorEvent類別* 」。

1. 載入播放內容所需的授權。
首先，嘗試載入本機儲存的授權來播放內容：

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android:DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   載入完成後，對象 `DRMManager` 將調度 `DRMStatusEvent.DRM_Status`。

1. 檢查對 `DRMVoucher` 像。


   如果對 `DRMVoucher` 像不是空值，則許可證有效。 轉至步驟9。

   [Android:DRMLicenseApparedCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS:DRMLicenseIncaptured](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. 檢查此內容的策略所需的驗證方法。

   使用屬 `DRMContentData.authenticationMethod` 性。
   1. 如果驗證方法 `ANONYMOUS`為，請轉至步驟9。 

      [Android:DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS:DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. 如果驗證方法為 `USERNAME_AND_PASSWORD`，您的應用程式必須提供讓使用者輸入憑證的機制。

      將使用者的認證傳遞至授權伺服器，以驗證使用者：

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      如果 `DRMManager` 驗證失 `DRMAuthenticationErrorEvent` 敗，則派單，或 `DRMAuthenticationCompleteEvent` 如果驗證成功。 為這些事件建立偵聽程式。

      [Android:authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS:驗證：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe建議使用更安全的機制來提供認證。 如需參考，請參 [閱KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html)。

   1. 如果驗證方法為 `UNKNOWN`，則必須使用自訂驗證方法。

      在這種情況下，內容提供者已安排以帶外方式進行驗證，而不是使用Primetime API。 自訂驗證程式必須產生可傳遞至方法的驗證Token `DRMManager.setAuthenticationToken()` 。

      [Android:setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS:setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >或者，無論使用何種驗證方法， `.setAuthenticationToken()` 都可用來將自訂資料從用戶端傳送至授權伺服器。 這是API的超載，因為此機制是在取得授權時，將動態自訂資料從用戶端傳送至授權伺服器的唯一方式。 在 [Primetime DRM(Adobe Access)論壇的數篇論壇文章中，對自訂資料傳輸方法有深入的討論 ](https://forums.adobe.com/community/adobe_access)。

1. 如果驗證失敗，您的應用程式必須返回步驟6。

   請確定您的應用程式有處理和限制重複驗證失敗的機制。 例如，在三次嘗試後，您會向使用者顯示訊息，指出驗證失敗且無法播放內容。
1. 若要使用儲存的Token，而非提示使用者輸入憑證，請使用方法來設定 `DRMManager.setAuthenticationToken()` Token。

   然後，您就可從授權伺服器下載授權，並像步驟6中一樣播放內容。
   1. **可選：** 如果驗證成功，您可擷取驗證Token，此為快取在記憶體中的位元組陣列。

      取得此Token與屬性 `DRMAuthenticationCompleteEvent.token` 一起。 您可以儲存和使用驗證Token，讓使用者不必重複輸入此內容的認證。 授權伺服器會決定驗證Token的有效期間。

      [Android:OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS:DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. 如果驗證成功，請從授權伺服器下載授權：

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   載入完成後，對象 `DRMManager` 將調度 `DRMStatusEvent.DRM_STATUS`。 監聽此事件，當它發送時，您可以播放內容。  建立Primetime物件並呼叫其方法，以播放視 `play()` 訊：

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android:acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)