---
title: 生成許可證
description: 生成許可證
copied-description: true
exl-id: 65c5677d-5a69-46f8-bc14-7af6d14d4dff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 生成許可證 {#generating-licenses}

要向用戶頒發葉許可證，SDK必須解密內容元資料中包含的CEK，並為請求許可證的電腦重新加密它。 要解密CEK，伺服器必須提供解密密鑰所需的資訊。 呼叫 `ContentInfo.setKeyRetrievalInfo()` 提供 `AsymmetricKeyRetrieval` 的雙曲餘切值。 如果元資料包含多個策略，則伺服器必須確定要使用和調用的策略 `LicenseRequestMessage.setSelectedPolicy()`。 然後打電話 `LicenseRequestMessage.generateLicense()` 以生成許可證。 使用 `License` 返回的對象，您可以修改許可證的過期或權限。

如果在 `ContentInfo` 對象，則許可證伺服器應使用關聯的CEK ID來獲取將插入到許可證中的相應CEK。 有關如何使用外部CEK工作流的詳細資訊，請參閱 [Adobe訪問DRM外部CEK概述](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
