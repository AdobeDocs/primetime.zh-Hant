---
title: 增強授權鏈結
description: 增強授權鏈結
copied-description: true
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 增強授權鏈結 {#enhanced-license-chaining}

如果使用DRM原則來產生支援授權鏈結的授權，則伺服器必須決定是核發Leaf授權、Root授權，還是兩者都核發。 如果要確定DRM原則支援的授權鏈結型別，您必須使用 `Policy.getLicenseChainType()`，或呼叫 `Policy.getRootLicenseId()` 以判斷DRM原則是否具有根授權。 透過Adobe Primetime DRM 2.0授權鏈結，伺服器通常會在使用者第一次請求特定機器的授權時發出Leaf授權，之後再請求根授權。 如果您要判斷電腦是否已擁有指定原則的Leaf授權，您需要呼叫 `LicenseRequestMessage.clientHasLeafForPolicy()`.

透過Adobe Primetime DRM 3.0中的增強型授權鏈結，建議在使用者第一次請求特定電腦的授權時同時核發Leaf和Root。 如果使用者已經擁有Root授權，伺服器可能只會發出Leaf (呼叫 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 以判斷使用者端是否已具有3.0 Enhanced Root)。 若是後續的授權要求，使用者端會指出它已有分葉和根，所以伺服器應該核發新的根授權。 使用增強型授權鏈結時， `setRootKeyRetrievalInfo()` 必須呼叫以提供在DRM原則中解密根加密金鑰所需的認證。

>[!NOTE]
>
>如果原則支援3.0 Enhanced License Chaining，但使用者端是Primetime DRM 2.0，則伺服器會發出2.0原始鏈結授權。 若要判斷使用者端版本，請使用 `LicenseRequestMessage.getClientVersion()`.
