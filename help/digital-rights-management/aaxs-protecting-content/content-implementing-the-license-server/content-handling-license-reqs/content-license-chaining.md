---
title: 授權鏈結
description: 授權鏈結
copied-description: true
exl-id: 2f439e21-c748-45aa-a87c-36e70ee3722a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 授權鏈結{#license-chaining}

如果用來產生授權的原則支援授權鏈結，則伺服器必須決定是核發Leaf授權、Root授權，還是兩者都核發。 若要判斷原則支援的授權鏈結型別，請使用 `Policy.getLicenseChainType()`，或呼叫 `Policy.getRootLicenseId()` 以判斷原則是否有根授權。 透過Adobe存取2.0授權鏈結，伺服器通常會在使用者第一次請求特定電腦的授權時發出分葉授權，之後再請求根授權。 若要判斷電腦是否已擁有指定原則的分葉授權，請呼叫 `LicenseRequestMessage.clientHasLeafForPolicy()`.
