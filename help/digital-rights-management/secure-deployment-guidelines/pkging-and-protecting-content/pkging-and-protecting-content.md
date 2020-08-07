---
description: 有關內容封裝與保護的資訊可讓您保護內容。
seo-description: 有關內容封裝與保護的資訊可讓您保護內容。
seo-title: 包裝和保護內容
title: 包裝和保護內容
uuid: 9bf89f86-082e-40f9-8deb-c9774a9d8e02
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# 封裝和保護內容 {#packaging-protecting-content}

有關內容封裝與保護的資訊可讓您保護內容。

## 保護伺服器的安全 {#securing-the-server}

您需要在物理上保護進行策略管理和內容打包的電腦。

如需詳細資訊，請參 [閱實體安全與存取](../../secure-deployment-guidelines/physical-sec-and-access.md)。

如果您的內容封裝實作需要網路連線，您必須加強作業系統並建置適當的防火牆解決方案。 有關詳細資訊，請參 [閱網路拓撲](../../secure-deployment-guidelines/overview/network-topology.md)。

## 安全地封裝內容 {#securely-packaging-content}

Adobe Primetime DRM Media Packager命令列工具的設定檔需要封裝期間使用的PKCS12憑證。

在Reference Implementation命令碼工具中，PKCS12憑據檔案的口令以明文形式儲存在 `flashaccess.properties` 檔案中。 因此，當您保護存放此檔案的電腦並確保電腦在安全的環境中時，請格外小心。 如需詳細資訊，請參 [閱實體安全與存取](../../secure-deployment-guidelines/physical-sec-and-access.md)。

封裝程式也會使用「授權伺服器」和「授權伺服器傳輸」憑證，而且必須保護這些資訊的完整性和機密性。 僅允許授權實體使用封裝程式。 如果您的私密金鑰受到危害，請立即通知Adobe Systems Incorporated，以便撤銷憑證。

>[!NOTE]
>
>API可讓您對多個內容使用相同的金鑰。 為確保最高等級的安全性，您只應將此功能用於多位元速率的FMS內容。 請勿對代表不同內容的多個檔案使用相同的索引鍵。

Primetime DRM封裝API會在特定條件下發出警告。 請檢閱這些警告，以判斷您的檔案是否已成功加密。 警告訊息可能是下列其中一項：

* 原則已過期，無法加密無法識別的標籤或追蹤。
* 無法加密影片片段，而這些片段中的參照可能無效。
* 中繼資料無法加密。

如果內容是使用具有錯誤屬性的原則來封裝，則必須更新原則。 更新的原則必須透過原則更新清單或其他傳送機制提供給授權伺服器。 建立策略後，無法更改某些策略屬性。 如果這些屬性不正確，請從散發網站拉回內容、撤銷原則，以便日後不能授與任何授權，然後再次加密內容。

封裝完成時，封裝金鑰會被廢棄項目收集，且不會明確銷毀。 因此，封裝鍵在記憶體中維持一段時間。 您必須防止未授權存取機器，並確保不會公開任何可能揭露此資訊的檔案，例如核心轉儲。

## 安全地儲存策略 {#securely-storing-policies}

Adobe Primetime DRM SDK可讓您開發可用於內容封裝和原則建立的應用程式。

當您建立這些應用程式時，您可以允許部分使用者建立和修改原則，並限制其他使用者僅將現有原則套用至內容。 您必須實施必要的存取控制，並建立具有不同權限的使用者帳戶，才能建立原則和原則應用程式。

在打包中使用策略之前，不會對其進行簽名或保護其不受修改。 如果您擔心打包工具用戶可能修改策略，請簽署策略以確保不能修改策略。

如需有關使用SDK建立應用程式的詳細資訊，請參閱 [API Primetime API參考上的Primetime DRM API](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)。

## 非對稱密鑰加密 {#asymmetric-key-encryption}

非對稱密鑰加密（也稱為公鑰加密）使用對密鑰。 一個密鑰用於加密，另一個密鑰用於解密。

解密密鑰或解密密鑰 *`private key`*&#x200B;被保密；加密金鑰或加密金 *`public key`*&#x200B;鑰可供任何有權加密內容的人使用。 任何可存取公開金鑰的人，都可以加密內容。 但是，只有具有私密金鑰存取權的人才能解密內容。 無法從公鑰重建私鑰。

當您封裝內容時，授權伺服器的公開金鑰會用來加密DRM中繼資料中的內容加密金鑰(CEK)。 您必須確保只有授權伺服器才能存取授權伺服器的私密金鑰。 如果其他人有密鑰，他們可以解密並查看內容。

>[!CAUTION]
>
>請務必從受信任來源取得包含公開金鑰的授權伺服器憑證。 這樣，您可以確保它是許可證伺服器的密鑰，而不是無管理的公共密鑰。 如果攻擊者用其公共密鑰替換許可證伺服器的密鑰，他們可以解密您的內容。

如需如何封裝內容的詳細資訊，請參 [閱「使用Adobe Primetime DRM SDK for Protecting Content](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf)」。