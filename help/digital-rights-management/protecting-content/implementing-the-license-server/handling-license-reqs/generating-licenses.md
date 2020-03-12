---
seo-title: 產生授權
title: 產生授權
uuid: f91b0cc8-e0ed-4722-947b-22eb2bfba916
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 產生授權{#generating-licenses}

如果您想要向使用者核發葉片授權，SDK必須解密內容中繼資料中包含的CEK，並重新加密該CEK，以供要求授權的機器使用。 要解密CEK，伺服器必須提供解密密鑰所需的資訊。 呼叫 `ContentInfo.setKeyRetrievalInfo()` 並提供物 `AsymmetricKeyRetrieval` 件。 如果中繼資料包含多個原則，伺服器必須決定要使用和呼叫的原則 `LicenseRequestMessage.setSelectedPolicy()`。 然後呼叫 `LicenseRequestMessage.generateLicense()` 以產生授權。 使用傳 `License` 回的物件，您可以修改授權的有效期或權限。

如果 `ExternalKeyRetrieval` 對象中指定了對 `ContentInfo` 像，則許可證伺服器應使用關聯的CEK ID來檢索插入到許可證中的相應CEK。

如需如 [何使用外部CEK工作流程的詳細資訊，請參閱](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) 「Adobe Primetime DRM外部CEK概觀」。
