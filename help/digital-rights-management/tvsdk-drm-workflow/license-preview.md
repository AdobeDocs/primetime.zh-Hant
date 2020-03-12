---
seo-title: 授權預覽
title: 授權預覽
uuid: 61ff171f-b977-40ef-8e8d-2900316fa89a
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 授權預覽 {#license-preview}

如果裝置是否可使用並完全執行Primetime DRM授權有任何問題，您可以使用「授權預覽」功能。 「預覽」授權完全符合最終授權中定義的所有限制和限制，但不包含解密受保護內容所需的內容加密金鑰(CEK)。 這項功能對於判斷用戶端是否確實可在內容授權代理商決定提供特定授權給用戶端之前使用授權非常有用。 例如——客戶希望觀看HD內容，但內容配銷商希望確保裝置可完整偵測並吸引HDCP。 在這種情況下，客戶可以呼叫 `DRMManager.loadPreviewVoucher()`。 如果收 `DRMStatusEvent` 到，而非收到 `DRMErrorEvent`，則確認用戶端可在授權中完全執行輸出保護限制，而內容授權代理商可自由提供此類授權給用戶端。

[iOS acquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
