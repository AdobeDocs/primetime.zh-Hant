---
description: 有關內容打包和保護的資訊使您能夠保護您的內容。
title: 包裝和保護內容
exl-id: f33d382b-07d7-4630-9e44-820d6249fee4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# 打包和保護內容 {#packaging-protecting-content}

有關內容打包和保護的資訊使您能夠保護您的內容。

## 保護伺服器 {#securing-the-server}

您需要對執行策略管理和內容打包的電腦進行物理保護。

有關詳細資訊，請參見 [物理安全和訪問](../../secure-deployment-guidelines/physical-sec-and-access.md)。

如果內容打包實施需要網路連接，則必須強化作業系統並實施適當的防火牆解決方案。 有關詳細資訊，請參見 [網路拓撲](../../secure-deployment-guidelines/overview/network-topology.md)。

## 安全地打包內容 {#securely-packaging-content}

Adobe PrimetimeDRM Media Packager命令行工具的配置檔案需要打包期間使用的PKCS12憑據。

在Reference Implementation（參考實現）命令級工具中，PKCS12憑據檔案的口令儲存在 `flashaccess.properties` 文本。 因此，在保護承載此檔案的電腦並確保電腦處於安全環境中時，應格外小心。 有關詳細資訊，請參見 [物理安全和訪問](../../secure-deployment-guidelines/physical-sec-and-access.md)。

打包程式還使用許可證伺服器和許可證伺服器傳輸證書，並且必須保護此資訊的完整性和機密性。 只應允許授權實體使用打包器。 如果您的私鑰被洩露，請立即通知Adobe Systems Incorporated，以便吊銷證書。

>[!NOTE]
>
>API使您能夠對多個內容使用相同的密鑰。 要確保最高級別的安全性，您應僅將此功能用於多比特率FMS內容。 不要對表示不同內容的多個檔案使用相同的密鑰。

黃金時段DRM打包API在特定條件下發出警告。 查看這些警告以確定您的檔案是否已成功加密。 警告消息可能是以下之一：

* 策略已過期，無法加密無法識別的標籤或跟蹤。
* 無法對影片片段進行加密，且這些片段中的引用可能無效。
* 無法加密元資料。

如果內容是通過使用屬性不正確的策略打包的，則需要更新策略。 必須通過策略更新清單或其他傳遞機制將更新的策略提供給許可證伺服器。 建立策略後，無法更改某些策略屬性。 如果這些屬性不正確，請從分發站點中撤回內容，撤消策略，以便將來不能授予許可證，然後重新加密內容。

包裝完成後，包裝密鑰被垃圾收集，不會被明確銷毀。 因此，封裝密鑰在記憶體中保留一段時間。 您必須防止對電腦進行未經授權的訪問，並確保不會洩露任何可能洩露此資訊的檔案。

## 安全地儲存策略 {#securely-storing-policies}

Adobe PrimetimeDRM SDK允許您開發可用於內容打包和策略建立的應用程式。

在建立這些應用程式時，您可以允許某些用戶建立和修改策略，並限制其他用戶僅將現有策略應用於內容。 您必須實施必要的訪問控制，並建立具有不同權限的用戶帳戶以建立策略和策略應用程式。

在打包中使用策略之前，不會對其進行簽名或保護以使其不受修改。 如果您擔心打包工具用戶可能修改策略，請簽署策略以確保策略無法修改。

有關使用SDK建立應用程式的詳細資訊，請參閱上的Mighine DRM API [API黃金時段API參考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)。

## 非對稱密鑰加密 {#asymmetric-key-encryption}

非對稱密鑰加密（也稱為公鑰加密）使用對密鑰。 一個密鑰用於加密，另一個密鑰用於解密。

解密密鑰，或 *`private key`*，保密；加密密鑰，或 *`public key`*，可供任何有權加密內容的人使用。 任何有權訪問公鑰的人都可以加密內容。 但是，只有有權訪問私鑰的人才能解密內容。 無法從公鑰重建私鑰。

打包內容時，許可證伺服器的公鑰將用於加密DRM元資料中的內容加密密鑰(CEK)。 必須確保只有許可證伺服器才能訪問許可證伺服器的私鑰。 如果其他人有密鑰，他們可以解密並查看內容。

>[!CAUTION]
>
>確保從受信任的源獲取包含公鑰的許可證伺服器證書。 這樣，您就可以確保它是許可證伺服器的密鑰，而不是無管理公鑰。 如果攻擊者用其公鑰替換許可證伺服器的密鑰，他們可以解密您的內容。

有關如何打包內容的詳細資訊，請參見 [使用Adobe PrimetimeDRM SDK保護內容](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf)。
