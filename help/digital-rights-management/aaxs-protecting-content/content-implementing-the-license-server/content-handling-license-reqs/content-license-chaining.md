---
title: 授權鏈結
description: 授權鏈結
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 授權鏈結{#license-chaining}

如果用來產生授權的原則支援授權鏈結，伺服器必須決定要核發Leaf授權、Root授權或兩者。 要確定策略支援的許可證連結類型，請使用`Policy.getLicenseChainType()`或調用`Policy.getRootLicenseId()`來確定策略是否具有根許可證。 使用Adobe存取2.0授權鏈，伺服器通常會在使用者第一次要求特定機器的授權時，核發葉片授權，並在此之後核發根授權。 要確定電腦是否已具有指定策略的葉許可證，請調用`LicenseRequestMessage.clientHasLeafForPolicy()`。
