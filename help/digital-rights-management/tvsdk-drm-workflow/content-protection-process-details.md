---
title: 許可證獲取流程詳細資訊
description: 許可證獲取流程詳細資訊
copied-description: true
exl-id: d772339a-8d05-401b-b5c1-18169b3627b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 許可證獲取流程詳細資訊 {#license-acquisition-process-details}

此過程提供黃金時段DRM保護內容工作流的詳細API級視圖：

1. 使用 `URLLoader` 對象，載入受保護內容的元資料檔案的位元組。

   將此對象設定為變數，如 `metadata_bytes`。 黃金時段DRM控制的所有內容都具有黃金時段DRM元資料。 在打包內容時，此元資料可以另存為單獨的元資料檔案( [!DNL .metadata])。 或者，元資料可以是Base64編碼的並插入到視頻清單檔案的主體中。 有關詳細資訊，請參見 [打包介質檔案](../protecting-content/packaging-media-overview/packaging-media-files.md)。
   1. 如有必要，請刪除感嘆號 `!` 從字串的開頭開始。
   1. 如果對於HLS或HDS內容有必要，請將Base64編碼字串中包含的元資料解碼為二進位資料，然後再將其傳遞。
1. 建立 `DRMContentData` 實例。

   將此代碼放入try-catch塊：

   ```
   new DRMContentData(metadata_bytes)
   ```

   何處 `metadata_bytes` 是 `URLLoader` 在步驟1中獲取的對象。

   [iOS:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. 建立監聽器以監聽 `DRMStatusEvent` 和 `DRMErrorEvent` 從 `DRMManager` 的雙曲餘切值。

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   在 `DRMStatusEvent` 監聽器，檢查許可證是否有效（非空）。 在 `DRMErrorEvent` 偵聽器，句柄 `DRMErrorEvents`。 請參閱 *使用DRMStatusEvent類* 和 *使用DRMErrorEvent類* 的子菜單。

1. 載入播放內容所需的許可證。
首先，嘗試載入本地儲存的許可證以播放內容：

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android:DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   載入完成後， `DRMManager` 對象調度 `DRMStatusEvent.DRM_Status`。

1. 檢查 `DRMVoucher` 的雙曲餘切值。


   如果 `DRMVoucher` 對象不為null，許可證有效。 轉至步驟9。

   [Android:DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS:DRMLicenseCapived](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. 檢查此內容的策略所需的身份驗證方法。

   使用 `DRMContentData.authenticationMethod` 屬性。
   1. 如果驗證方法為 `ANONYMOUS`，轉到步驟9。 

      [Android:DRMAuthentication方法](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS:DRMAuthentication方法](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. 如果驗證方法為 `USERNAME_AND_PASSWORD`，您的應用程式必須提供允許用戶輸入憑據的機制。

      將用戶的憑據傳遞給許可證伺服器以驗證用戶：

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      的 `DRMManager` 派單 `DRMAuthenticationErrorEvent` 如果驗證失敗，或 `DRMAuthenticationCompleteEvent` 驗證成功。 為這些事件建立偵聽器。

      [Android:authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS:驗證：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe建議使用更安全的機制來提供憑據。 有關參考，請參見 [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html)。

   1. 如果驗證方法為 `UNKNOWN`，必須使用自定義身份驗證方法。

      在這種情況下，內容提供者已經安排以帶外方式進行驗證，而不是使用黃金時段API。 自定義身份驗證過程必須生成可傳遞給 `DRMManager.setAuthenticationToken()` 的雙曲餘切值。

      [Android:setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS:setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >或者，無論身份驗證方法如何， `.setAuthenticationToken()` 可用於將自定義資料從客戶端發送到許可證伺服器。 這是API的過載，因為此機制是在獲取許可證時將動態自定義資料從客戶端發送到許可證伺服器的唯一方法。 此定制資料傳輸方法在以下幾個論壇帖子中深入討論 [黃金時段DRM(Adobe訪問)論壇 ](https://forums.adobe.com/community/adobe_access)。

1. 如果驗證失敗，則您的應用程式必須返回步驟6。

   確保您的應用程式具有處理和限制重複身份驗證失敗的機制。 例如，在三次嘗試後，您將向用戶顯示一條消息，指出身份驗證失敗且無法播放內容。
1. 要使用儲存的令牌而不是提示用戶輸入憑據，請使用 `DRMManager.setAuthenticationToken()` 的雙曲餘切值。

   然後，您將從許可證伺服器下載許可證並按步驟6中的步驟播放內容。
   1. **可選：** 如果驗證成功，可以捕獲驗證令牌，該令牌是快取在記憶體中的位元組陣列。

      使用 `DRMAuthenticationCompleteEvent.token` 屬性。 您可以儲存和使用身份驗證令牌，以便用戶不必重複輸入此內容的憑據。 許可證伺服器確定驗證令牌的有效期。

      [Android:OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS:DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. 如果驗證成功，請從許可證伺服器下載許可證：

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   載入完成後， `DRMManager` 對象調度 `DRMStatusEvent.DRM_STATUS`。 收聽此活動，當它被分派時，您可以播放內容。  通過建立黃金時段對象並調用其來播放視頻 `play()` 方法：

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
