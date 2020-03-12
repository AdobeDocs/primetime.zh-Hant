---
seo-title: 產生授權
title: 產生授權
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 產生授權 {#generating-licenses}

若要向使用者核發葉片授權，SDK必須解密內容中繼資料中包含的CEK，並重新加密該CEK，以供要求授權的機器使用。 要解密CEK，伺服器必須提供解密密鑰所需的資訊。 呼叫 `ContentInfo.setKeyRetrievalInfo()` 並提供物 `AsymmetricKeyRetrieval` 件。 如果中繼資料包含多個原則，伺服器必須決定要使用和呼叫的原則 `LicenseRequestMessage.setSelectedPolicy()`。 然後呼叫 `LicenseRequestMessage.generateLicense()` 以產生授權。 使用傳 `License` 回的物件，您可以修改授權的有效期或權限。

如果在物件中指定ExternalKeyRetrieval物件，則 `ContentInfo` 授權伺服器應使用相關的CEK ID來擷取將插入授權的適當CEK。 如需如何使用外部CEK工作流程的詳細資訊，請參 [閱Adobe Access DRM External CEK概觀](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
