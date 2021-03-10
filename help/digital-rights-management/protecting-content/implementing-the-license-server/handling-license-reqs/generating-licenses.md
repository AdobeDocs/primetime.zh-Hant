---
title: 產生授權
description: 產生授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# 產生授權{#generating-licenses}

如果您想要向使用者核發葉片授權，SDK必須解密內容中繼資料中包含的CEK，並重新加密該CEK，以供要求授權的機器使用。 要解密CEK，伺服器必須提供解密密鑰所需的資訊。 呼叫`ContentInfo.setKeyRetrievalInfo()`並提供`AsymmetricKeyRetrieval`物件。 如果元資料包含多個策略，則伺服器必須確定要使用哪個策略並調用`LicenseRequestMessage.setSelectedPolicy()`。 然後呼叫`LicenseRequestMessage.generateLicense()`以產生授權。 使用傳回的`License`物件，您可以修改授權的有效期或權限。

如果在`ContentInfo`物件中指定`ExternalKeyRetrieval`物件，則授權伺服器應使用相關的CEK ID來擷取插入授權的適當CEK。

如需如何使用外部CEK工作流程的詳細資訊，請參閱[Adobe PrimetimeDRM外部CEK概述](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)。
