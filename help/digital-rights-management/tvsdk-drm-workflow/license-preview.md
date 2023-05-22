---
title: 許可證預覽
description: 許可證預覽
copied-description: true
exl-id: 53a57610-86a8-4c5d-9494-679ede35abf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 許可證預覽 {#license-preview}

如果設備是否可以使用和完全強制使用黃金時段DRM許可證存在問題，則可以使用許可證預覽功能。 預覽許可證完全匹配最終許可證中定義的所有約束和限制，但不包含解密受保護內容所需的內容加密密鑰(CEK)。 此功能在內容分發伺服器決定向客戶端提供特定許可證之前確定是否確實可以使用許可證時非常有用。 例如 — 客戶希望觀看高清內容，但內容分發商希望確保設備能夠完全檢測並參與HDCP。 在這種情況下，客戶端可以 `DRMManager.loadPreviewVoucher()`。 如果 `DRMStatusEvent` 接收，而不是 `DRMErrorEvent`然後，確認客戶端可以在許可證中完全強制實施輸出保護限制，並且內容分發伺服器可以自由地向客戶端提供此類許可證。

[iOSacquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
