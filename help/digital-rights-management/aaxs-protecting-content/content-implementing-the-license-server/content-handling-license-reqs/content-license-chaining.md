---
title: 授權鏈結
description: 授權鏈結
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 授權鏈結{#license-chaining}

如果用於產生授權的原則支援授權鏈結，則伺服器必須決定要核發Leaf授權、Root授權，或兩者都核發。 若要判斷原則支援的授權鏈結型別，請使用 `Policy.getLicenseChainType()`，或呼叫 `Policy.getRootLicenseId()` 以判斷原則是否具有根授權。 透過Adobe存取2.0授權鏈結，伺服器通常會在使用者第一次請求特定電腦的授權時發出葉授權，並在之後發出根授權。 若要判斷電腦是否已擁有指定原則的分葉授權，請呼叫 `LicenseRequestMessage.clientHasLeafForPolicy()`.
