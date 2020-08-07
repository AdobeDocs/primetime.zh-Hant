---
seo-title: 增強的授權鏈結
title: 增強的授權鏈結
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 增強的授權鏈結 {#enhanced-license-chaining}

在Adobe Access 3.0中增強的授權鏈結，建議使用者在第一次要求特定機器的授權時，同時核發Leaf和Root。 如果使用者已擁有根授權，伺服器可能只會發出葉( `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 呼叫以判斷用戶端是否已擁有3.0增強根)。 對於後續的授權要求，用戶端會指出其已有Leaf和Root，因此伺服器應該會核發新的Root授權。 當使用增強的授權連結時， `setRootKeyRetrievalInfo()` 必須呼叫，以提供解密策略中的根加密密鑰所需的憑據。

>[!NOTE]
>
>如果原則支援3.0增強授權鏈結，但用戶端是Adobe Access 2.0，則伺服器會核發2.0原始鏈結授權。 要確定客戶端版本，請使用LicenseRequestMessage.getClientVersion()。

