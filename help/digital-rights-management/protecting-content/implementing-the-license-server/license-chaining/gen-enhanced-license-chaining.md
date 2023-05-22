---
title: 增強的許可證連結
description: 增強的許可證連結
copied-description: true
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 增強的許可證連結 {#enhanced-license-chaining}

如果使用DRM策略生成支援許可證連結的許可證，則伺服器必須決定是發放葉許可證、根許可證還是兩者兼有。 如果要確定DRM策略支援的許可連結類型，必須使用 `Policy.getLicenseChainType()`或 `Policy.getRootLicenseId()` 確定DRM策略是否具有根許可。 利用Adobe PrimetimeDRM 2.0許可鏈，伺服器通常在用戶第一次請求特定機器的許可時發出葉許可，並且隨後發出根許可。 如果要確定電腦是否已具有指定策略的葉許可證，則需要調用 `LicenseRequestMessage.clientHasLeafForPolicy()`。

通過在Adobe PrimetimeDRM 3.0中增強的許可連結，建議在用戶第一次請求特定電腦的許可時同時發出葉和根。 如果用戶已擁有根許可證，則伺服器可能僅發出葉（調用） `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 確定客戶端是否已具有3.0增強根)。 對於後續的許可證請求，客戶端隨後會指示它已經具有葉和根，因此伺服器應頒發新的根許可證。 使用增強的許可證連結時， `setRootKeyRetrievalInfo()` 必須調用以提供解密DRM策略中的根加密密鑰所需的憑據。

>[!NOTE]
>
>如果策略支援3.0增強版許可連結，但客戶端是黃金時段DRM 2.0，則伺服器隨後會發出2.0原始版連結許可。 要確定客戶端版本，請使用 `LicenseRequestMessage.getClientVersion()`。
