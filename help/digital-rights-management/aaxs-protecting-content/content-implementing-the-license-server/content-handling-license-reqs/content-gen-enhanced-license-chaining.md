---
title: 增強的許可證連結
description: 增強的許可證連結
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 增強的許可證連結 {#enhanced-license-chaining}

在AdobeAccess 3.0中通過增強的許可證連結，建議在用戶首次請求特定電腦的許可證時同時發出葉和根。 如果用戶已擁有根許可證，則伺服器可能僅發出葉（調用） `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 確定客戶端是否已具有3.0增強根)。 對於後續的許可證請求，客戶端將指示它已經具有葉和根，因此伺服器應頒發新的根許可證。 使用增強的許可證連結時， `setRootKeyRetrievalInfo()` 必須調用以提供解密策略中的根加密密鑰所需的憑據。

>[!NOTE]
>
>如果策略支援3.0增強的許可證連結，但客戶端是Adobe訪問2.0，則伺服器將頒發2.0原始連結許可證。 要確定客戶端版本，請使用LicenseRequestMessage.getClientVersion()。
