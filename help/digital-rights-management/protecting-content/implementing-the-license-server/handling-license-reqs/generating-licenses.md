---
title: 正在產生授權
description: 正在產生授權
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 正在產生授權{#generating-licenses}

如果您想要向使用者核發分葉授權，SDK必須解密內容中繼資料中包含的CEK，並為請求授權的電腦重新加密。 若要解密CEK，伺服器必須提供解密金鑰所需的資訊。 呼叫 `ContentInfo.setKeyRetrievalInfo()` 並提供 `AsymmetricKeyRetrieval` 物件。 如果中繼資料包含多個原則，伺服器必須決定要使用哪個原則並呼叫 `LicenseRequestMessage.setSelectedPolicy()`. 然後呼叫 `LicenseRequestMessage.generateLicense()` 以產生授權。 使用 `License` 傳回的物件，您可以修改授權中的到期日或權利。

如果 `ExternalKeyRetrieval` 物件指定於 `ContentInfo` 物件，則許可證伺服器應使用關聯的CEK ID來擷取插入許可證中的適當CEK。

請參閱 [Adobe Primetime DRM外部CEK概觀](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) 瞭解更多如何使用外部CEK工作流程的詳細資訊。
