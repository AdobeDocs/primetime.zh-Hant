---
title: 授權預覽
description: 授權預覽
copied-description: true
exl-id: 53a57610-86a8-4c5d-9494-679ede35abf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 授權預覽 {#license-preview}

如果有關於裝置是否可以使用和完全強制執行Primetime DRM授權的問題，您可以使用「授權預覽」功能。 預覽授權完全符合最終授權中定義的所有限制和限制，但不包含解密受保護內容所需的內容加密金鑰(CEK)。 此功能有助於在內容散發者決定向使用者端提供特定授權之前，判斷使用者端是否確實可以使用授權。 例如，客戶想要觀賞HD內容，但內容經銷商想要確保裝置可以完全偵測並接合HDCP。 在此情況下，使用者端可以呼叫 `DRMManager.loadPreviewVoucher()`. 若為 `DRMStatusEvent` 「 」會收到，而不是 `DRMErrorEvent`，則使用者端可完全強制執行授權中的輸出保護限制，且內容散發者可免費將此型別的授權提供給使用者端。

[iOS acquirePreviewLicense：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
