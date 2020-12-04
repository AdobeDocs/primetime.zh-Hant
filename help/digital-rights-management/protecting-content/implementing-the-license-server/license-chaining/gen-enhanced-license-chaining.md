---
seo-title: 增強的授權鏈結
title: 增強的授權鏈結
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 增強的授權鏈{#enhanced-license-chaining}

如果使用DRM政策來產生支援授權鏈結的授權，伺服器必須決定是要核發Leaf授權、Root授權或兩者。 如果想要確定DRM策略支援的許可連結類型，必須使用`Policy.getLicenseChainType()`或調用`Policy.getRootLicenseId()`來確定DRM策略是否具有根許可。 使用Adobe Primetime DRM 2.0授權鏈結時，伺服器通常會在使用者第一次要求特定機器的授權時發出葉片授權，並在此之後發出根授權。 如果要確定電腦是否已具有指定策略的葉許可證，則需要調用`LicenseRequestMessage.clientHasLeafForPolicy()`。

Adobe Primetime DRM 3.0中增強的授權鏈結，建議使用者在第一次要求特定機器的授權時同時核發Leaf和Root。 如果用戶已經擁有Root許可證，則伺服器僅能發出Leaf（調用`LicenseRequestMessage.clientHasEnhancedRootForPolicy()`以確定客戶機是否已擁有3.0 Enhanced Root）。 對於後續的授權要求，用戶端會指出其已有Leaf和Root，因此伺服器應發行新的Root授權。 使用增強的授權連結時，必須調用`setRootKeyRetrievalInfo()`以提供解密DRM策略中的根加密密鑰所需的憑據。

>[!NOTE]
>
>如果原則支援3.0增強授權鏈結，但用戶端是Primetime DRM 2.0，則伺服器會發出2.0原始鏈結授權。 要確定客戶端版本，請使用`LicenseRequestMessage.getClientVersion()`。

