---
description: 有關封裝和保護內容的資訊，可讓您保護內容。
title: 包裝與保護內容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# 包裝和保護內容 {#packaging-protecting-content}

有關封裝和保護內容的資訊，可讓您保護內容。

## 保護伺服器 {#securing-the-server}

您需要實際保護發生原則管理和內容封裝的電腦。

如需詳細資訊，請參閱 [實體安全性與存取權](../../secure-deployment-guidelines/physical-sec-and-access.md).

如果您的內容封裝實作需要網路連線，則必須強化作業系統，並實作適當的防火牆解決方案。 如需詳細資訊，請參閱 [網路拓撲](../../secure-deployment-guidelines/overview/network-topology.md).

## 安全地封裝內容 {#securely-packaging-content}

Adobe Primetime DRM Media Packager命令列工具的組態檔需要封裝期間使用的PKCS12認證。

在「參考實作」命令列工具中，PKCS12認證檔案的密碼會儲存在 `flashaccess.properties` 以純文字顯示的檔案。 因此，當您保護裝載此檔案的電腦時，請格外小心，並確保電腦處於安全的環境中。 如需詳細資訊，請參閱 [實體安全性與存取權](../../secure-deployment-guidelines/physical-sec-and-access.md).

封裝程式也使用License Server和License Server傳輸憑證，而且必須保護此資訊的完整性和機密性。 只允許授權實體使用封裝程式。 如果您的私密金鑰遭到盜用，請立即通知Adobe Systems Incorporated以撤銷憑證。

>[!NOTE]
>
>此API可讓您針對多個內容片段使用相同的金鑰。 為了確保最高等級的安全性，您應該只在多位元速率FMS內容中使用此功能。 請勿對代表不同內容的多個檔案使用相同金鑰。

Primetime DRM Packaging API會在某些情況下發出警告。 請檢閱這些警告，以判斷您的檔案是否已成功加密。 警告訊息可能是下列其中一項：

* 原則已過期，且無法加密無法辨識的標籤或追蹤。
* 無法加密影片片段，且這些片段內的參考可能無效。
* 中繼資料無法加密。

如果使用屬性不正確的原則封裝內容，則需要更新原則。 更新的原則必須透過原則更新清單或其他傳遞機制提供給License Server。 建立原則之後，就無法變更某些原則屬性。 如果這些屬性不正確，請從發佈網站提取內容、撤銷原則以便未來無法授與授權，然後再次加密內容。

封裝完成時，封裝金鑰會遭到廢棄專案收集，且不會明確銷毀。 因此，封裝金鑰會保留在記憶體中一段時間。 您必須防止未經授權存取電腦，並確保不會公開任何可能洩露此資訊的檔案，例如核心傾印。

## 安全地儲存原則 {#securely-storing-policies}

Adobe Primetime DRM SDK可讓您開發可用於內容封裝和原則建立的應用程式。

當您建立這些應用程式時，您可以允許某些使用者建立和修改原則，並限制其他使用者只將現有原則套用至內容。 您必須實作必要的存取控制項，並建立具有不同許可權的使用者帳號，才能建立原則及套用原則。

原則在用於封裝之前，不會經過簽署或受到修改保護。 如果您擔心封裝工具使用者可能會修改原則，請簽署原則以確保無法修改原則。

如需有關使用SDK建立應用程式的詳細資訊，請參閱上的Primetime DRM API [API Primetime API參考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## 非對稱金鑰加密 {#asymmetric-key-encryption}

非對稱金鑰加密（也稱為公開金鑰加密）使用金鑰組。 一個金鑰用於加密，另一個金鑰用於解密。

解密金鑰，或 *`private key`*，會保密；加密金鑰或 *`public key`*，可供獲授權加密內容的任何人使用。 任何有權存取公開金鑰的人都可以加密內容。 不過，只有可存取私密金鑰的人才能解密內容。 無法從公開金鑰重建私密金鑰。

當您封裝內容時，會使用授權伺服器的公開金鑰來加密DRM中繼資料中的內容加密金鑰(CEK)。 您必須確保只有授權伺服器可以存取授權伺服器的私密金鑰。 如果其他人擁有金鑰，他們可以解密並檢視內容。

>[!CAUTION]
>
>請務必從信任的來源取得包含公開金鑰的License Server憑證。 如此一來，您便可確保該金鑰是License Server的金鑰，而非惡意公開金鑰。 如果攻擊者用他們的公開金鑰取代授權伺服器的金鑰，他們可以解密您的內容。

如需如何封裝內容的詳細資訊，請參閱 [使用Adobe Primetime DRM SDK來保護內容](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).
