---
seo-title: 授權鏈結
title: 授權鏈結
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 授權鏈結{#license-chaining}

如果用來產生授權的原則支援授權鏈結，伺服器必須決定要核發Leaf授權、Root授權或兩者。 要確定策略支援的許可證連結類型，請使 `Policy.getLicenseChainType()`用或調用 `Policy.getRootLicenseId()` 來確定策略是否具有根許可證。 使用Adobe Access 2.0授權鏈結，伺服器通常會在使用者第一次要求特定機器的授權時，核發葉片授權，並在此之後核發根授權。 要確定電腦是否已具有指定策略的葉許可證，請調用 `LicenseRequestMessage.clientHasLeafForPolicy()`。
