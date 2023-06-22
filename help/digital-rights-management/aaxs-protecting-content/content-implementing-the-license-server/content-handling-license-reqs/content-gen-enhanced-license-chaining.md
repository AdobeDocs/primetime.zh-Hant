---
title: 增強授權鏈結
description: 增強授權鏈結
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 增強授權鏈結 {#enhanced-license-chaining}

透過Adobe存取3.0的增強型授權鏈結，建議在使用者第一次請求特定電腦的授權時同時核發Leaf和Root。 如果使用者已經擁有Root授權，伺服器可能只會發出Leaf (呼叫 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 以判斷使用者端是否已具有3.0 Enhanced Root)。 對於後續的授權要求，使用者端會指出它已經有分葉和根，所以伺服器應該核發新的根授權。 使用增強型授權鏈結時， `setRootKeyRetrievalInfo()` 必須呼叫以提供在原則中解密根加密金鑰所需的認證。

>[!NOTE]
>
>如果原則支援3.0 Enhanced License Chaining，但使用者端為Adobe存取2.0，則伺服器將核發2.0原始鏈結授權。 若要判斷使用者端版本，請使用LicenseRequestMessage.getClientVersion()。
