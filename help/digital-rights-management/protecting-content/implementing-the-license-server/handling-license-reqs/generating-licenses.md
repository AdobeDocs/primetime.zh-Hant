---
title: 生成許可證
description: 生成許可證
copied-description: true
exl-id: c47627b5-19de-41e5-8cb6-4084af714e09
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 生成許可證{#generating-licenses}

如果要向用戶頒發葉許可證，SDK必須解密內容元資料中包含的CEK，並為請求許可證的電腦重新加密它。 要解密CEK，伺服器必須提供解密密鑰所需的資訊。 呼叫 `ContentInfo.setKeyRetrievalInfo()` 提供 `AsymmetricKeyRetrieval` 的雙曲餘切值。 如果元資料包括多個策略，則伺服器必須確定要使用和調用的策略 `LicenseRequestMessage.setSelectedPolicy()`。 然後打電話 `LicenseRequestMessage.generateLicense()` 以生成許可證。 使用 `License` 返回的對象，您可以修改許可證的過期或權限。

如果 `ExternalKeyRetrieval` 對象在 `ContentInfo` 對象，則許可證伺服器應使用關聯的CEK ID來檢索插入到許可證中的相應CEK。

查看 [Adobe PrimetimeDRM外部CEK概述](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) 的子菜單。
