---
title: 許可證連結
description: 許可證連結
copied-description: true
exl-id: 2f439e21-c748-45aa-a87c-36e70ee3722a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 許可證連結{#license-chaining}

如果用於生成許可證的策略支援許可證連結，則伺服器必須決定是發放葉許可證、根許可證還是兩者兼有。 要確定策略支援的許可證連結類型，請使用 `Policy.getLicenseChainType()`或 `Policy.getRootLicenseId()` 確定策略是否具有根許可證。 通過Adobe訪問2.0許可證連結，伺服器通常在用戶第一次請求特定電腦的許可證時發出葉許可證，並在此後發出根許可證。 要確定電腦是否已具有指定策略的葉許可證，請調用 `LicenseRequestMessage.clientHasLeafForPolicy()`。
